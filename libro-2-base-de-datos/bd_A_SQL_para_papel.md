---
tags: [efip, base-de-datos, anexo, sql]
libro: 2
anexo: A
---

# A. SQL listo para papel

> [!info] Para qué sirve
> Lo que más se pide escribir a mano. Practicá sin mirar.

## A.1 DDL completo del caso

```sql
CREATE TABLE dispositivo (
    id        INT AUTO_INCREMENT PRIMARY KEY,
    codigo    VARCHAR(10) NOT NULL UNIQUE,
    tipo      VARCHAR(20) NOT NULL,
    ubicacion VARCHAR(100) NOT NULL,
    activo    BOOLEAN NOT NULL DEFAULT TRUE,
    CONSTRAINT ck_tipo CHECK (tipo IN ('semaforo','camara'))
);

CREATE TABLE alerta (
    id             INT AUTO_INCREMENT PRIMARY KEY,
    fecha          DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    mensaje        VARCHAR(200) NOT NULL,
    prioridad      TINYINT NOT NULL,
    atendida       BOOLEAN NOT NULL DEFAULT FALSE,
    id_dispositivo INT NOT NULL,
    CONSTRAINT ck_prio CHECK (prioridad BETWEEN 1 AND 5),
    CONSTRAINT fk_alerta_disp FOREIGN KEY (id_dispositivo)
        REFERENCES dispositivo(id) ON DELETE CASCADE
);

CREATE TABLE tecnico (
    id        INT AUTO_INCREMENT PRIMARY KEY,
    nombre    VARCHAR(60) NOT NULL,
    matricula VARCHAR(20) NOT NULL UNIQUE
);

CREATE TABLE reparacion (
    id         INT AUTO_INCREMENT PRIMARY KEY,
    fecha      DATE NOT NULL,
    costo      DECIMAL(10,2) NOT NULL DEFAULT 0,
    id_alerta  INT NOT NULL UNIQUE,
    id_tecnico INT NULL,
    CONSTRAINT ck_costo CHECK (costo >= 0),
    CONSTRAINT fk_rep_alerta FOREIGN KEY (id_alerta)
        REFERENCES alerta(id) ON DELETE CASCADE,
    CONSTRAINT fk_rep_tecnico FOREIGN KEY (id_tecnico)
        REFERENCES tecnico(id) ON DELETE SET NULL
);
```

## A.2 Consultas esenciales

```sql
-- 1. Proyección y filtro
SELECT codigo, ubicacion FROM dispositivo WHERE tipo = 'camara';

-- 2. Orden y límite
SELECT codigo FROM dispositivo ORDER BY codigo DESC LIMIT 3;

-- 3. Like
SELECT nombre FROM tecnico WHERE nombre LIKE 'L%';

-- 4. Nulos
SELECT id FROM reparacion WHERE id_tecnico IS NULL;

-- 5. Between
SELECT id FROM alerta WHERE prioridad BETWEEN 1 AND 2;

-- 6. In
SELECT codigo FROM dispositivo WHERE tipo IN ('semaforo','camara');

-- 7. Join simple
SELECT a.id, a.mensaje, d.codigo
FROM alerta a
JOIN dispositivo d ON d.id = a.id_dispositivo;

-- 8. Left join + contar (incluye ceros)
SELECT d.codigo, COUNT(a.id) AS alertas
FROM dispositivo d
LEFT JOIN alerta a ON a.id_dispositivo = d.id
GROUP BY d.codigo;

-- 9. Huérfanos
SELECT d.codigo
FROM dispositivo d
LEFT JOIN alerta a ON a.id_dispositivo = d.id
WHERE a.id IS NULL;

-- 10. Agrupamiento con having
SELECT d.codigo, COUNT(*) AS total
FROM dispositivo d
JOIN alerta a ON a.id_dispositivo = d.id
GROUP BY d.codigo
HAVING COUNT(*) > 2;

-- 11. Promedio y redondeo
SELECT ROUND(AVG(costo), 2) AS promedio FROM reparacion;

-- 12. Agrupar por mes
SELECT YEAR(fecha) AS anio, MONTH(fecha) AS mes, COUNT(*) AS total
FROM alerta
GROUP BY YEAR(fecha), MONTH(fecha)
ORDER BY anio, mes;

-- 13. Subconsulta escalar
SELECT nombre, sueldo
FROM empleado
WHERE sueldo > (SELECT AVG(sueldo) FROM empleado);

-- 14. IN con subconsulta
SELECT nombre
FROM empleado
WHERE id_depto IN (SELECT id_depto FROM departamento WHERE ciudad = 'La Plata');

-- 15. EXISTS
SELECT d.codigo
FROM dispositivo d
WHERE EXISTS (
    SELECT 1 FROM alerta a
    WHERE a.id_dispositivo = d.id AND a.prioridad = 1
);

-- 16. Autojuntura
SELECT e.nombre AS empleado, j.nombre AS jefe
FROM empleado e
LEFT JOIN empleado j ON j.legajo = e.id_jefe;

-- 17. Union
SELECT codigo AS id, 'dispositivo' AS origen FROM dispositivo
UNION
SELECT CAST(id AS CHAR), 'alerta' FROM alerta;

-- 18. Top N por grupo (MySQL 8)
SELECT *
FROM (
    SELECT d.codigo, a.mensaje,
           ROW_NUMBER() OVER (PARTITION BY d.id ORDER BY a.prioridad) AS rn
    FROM dispositivo d
    JOIN alerta a ON a.id_dispositivo = d.id
) t
WHERE rn <= 2;

-- 19. Actualizar con join
UPDATE alerta a
JOIN dispositivo d ON d.id = a.id_dispositivo
SET a.prioridad = 1
WHERE d.tipo = 'camara' AND a.prioridad = 2;

-- 20. Borrar con condición
DELETE FROM alerta WHERE prioridad = 5 AND fecha < '2026-01-01';
```

> [!warning] `ROW_NUMBER()` no está en el programa
> Se incluye para consultas de “top N por grupo”. Si la usás en el examen, aclará que es una función de ventana de MySQL 8; la alternativa clásica es una subconsulta con `COUNT`.

## A.3 Bloque PL/SQL

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_total NUMBER := 0;
    v_nombre empleado.nombre%TYPE;
BEGIN
    SELECT COUNT(*) INTO v_total FROM alerta WHERE prioridad = 1;

    SELECT nombre INTO v_nombre FROM empleado WHERE legajo = 1001;

    DBMS_OUTPUT.PUT_LINE('Críticas: ' || v_total);
    DBMS_OUTPUT.PUT_LINE('Empleado: ' || v_nombre);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No se encontró el empleado');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```

## A.4 Procedimiento y función

```sql
CREATE OR REPLACE PROCEDURE registrar_alerta (
    p_dispositivo IN NUMBER,
    p_mensaje     IN VARCHAR2,
    p_prioridad   IN NUMBER
) AS
BEGIN
    IF p_prioridad < 1 OR p_prioridad > 5 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Prioridad inválida');
    END IF;

    INSERT INTO alerta (mensaje, prioridad, id_dispositivo)
    VALUES (p_mensaje, p_prioridad, p_dispositivo);
END;
/
```

```sql
CREATE OR REPLACE FUNCTION cantidad_alertas (
    p_dispositivo IN NUMBER
) RETURN NUMBER IS
    v NUMBER;
BEGIN
    SELECT COUNT(*) INTO v FROM alerta WHERE id_dispositivo = p_dispositivo;
    RETURN v;
END;
/
```

## A.5 Cursor

```sql
DECLARE
    CURSOR c IS
        SELECT id, mensaje FROM alerta WHERE prioridad = 1;
    v_id      alerta.id%TYPE;
    v_mensaje alerta.mensaje%TYPE;
BEGIN
    OPEN c;
    LOOP
        FETCH c INTO v_id, v_mensaje;
        EXIT WHEN c%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE(v_id || ': ' || v_mensaje);
    END LOOP;
    CLOSE c;
END;
/
```

## A.6 Trigger de auditoría

```sql
CREATE OR REPLACE TRIGGER trg_alerta_aud
AFTER UPDATE OF prioridad ON alerta
FOR EACH ROW
BEGIN
    INSERT INTO auditoria_alerta
        (id_alerta, prioridad_old, prioridad_new, usuario, fecha)
    VALUES
        (:OLD.id, :OLD.prioridad, :NEW.prioridad, USER, SYSDATE);
END;
/
```

## A.7 Equivalente MySQL de un procedimiento

```sql
DELIMITER //

CREATE PROCEDURE registrar_alerta(
    IN p_dispositivo INT,
    IN p_mensaje VARCHAR(200),
    IN p_prioridad TINYINT
)
BEGIN
    IF p_prioridad < 1 OR p_prioridad > 5 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Prioridad inválida';
    END IF;

    INSERT INTO alerta (mensaje, prioridad, id_dispositivo)
    VALUES (p_mensaje, p_prioridad, p_dispositivo);
END //

DELIMITER ;

CALL registrar_alerta(1, 'Prueba', 2);
```

## A.8 Permisos

```sql
CREATE USER 'reportes'@'localhost' IDENTIFIED BY 'Clave2026!';
GRANT SELECT ON municipio.* TO 'reportes'@'localhost';
SHOW GRANTS FOR 'reportes'@'localhost';
REVOKE SELECT ON municipio.* FROM 'reportes'@'localhost';
```

#libro2 #anexo #sql
