---
tags: [efip, base-de-datos, cierre]
libro: 2
parte: 3
---

# Cierre del Módulo 3 — SQL

> [!info] Qué hacer con este archivo
> Verificación de DDL, DML, consultas y permisos. Si algo falla, volvé al capítulo.

## Checklist del Módulo 3

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Clasificar sentencias en DDL/DML/DCL | [[bd11_lenguaje-sql\|Cap. 11]] | ☐ |
| Nombrar objetos y constraints con convención | [[bd14_convenciones-y-tipos\|Cap. 14]] | ☐ |
| Elegir el tipo de dato correcto | [[bd14_convenciones-y-tipos\|Cap. 14]] | ☐ |
| Justificar DECIMAL vs. FLOAT | [[bd14_convenciones-y-tipos\|Cap. 14]] | ☐ |
| Explicar el orden lógico de una consulta | [[bd11_lenguaje-sql\|Cap. 11]] | ☐ |
| Crear una base y una tabla con restricciones | [[bd13_ddl\|Cap. 13]] | ☐ |
| Modificar una tabla con `ALTER` | [[bd13_ddl\|Cap. 13]] | ☐ |
| Diferenciar `DROP`, `TRUNCATE` y `DELETE` | [[bd13_ddl\|Cap. 13]] | ☐ |
| Insertar, actualizar y borrar con seguridad | [[bd12_dml\|Cap. 12]] | ☐ |
| Filtrar con `BETWEEN`, `IN`, `LIKE`, `IS NULL` | [[bd15_select\|Cap. 15]] | ☐ |
| Ordenar y paginar | [[bd15_select\|Cap. 15]] | ☐ |
| Unir tablas con `INNER`, `LEFT` y autojuntura | [[bd16_joins-subconsultas\|Cap. 16]] | ☐ |
| Resolver con subconsulta o `EXISTS` | [[bd16_joins-subconsultas\|Cap. 16]] | ☐ |
| Aplicar el método de 7 pasos a un enunciado | [[bd17_metodo-consultas\|Cap. 17]] | ☐ |
| Reconocer los patrones “no tiene” y “todos” | [[bd17_metodo-consultas\|Cap. 17]] | ☐ |
| Agrupar y filtrar grupos con `HAVING` | [[bd18_agrupamiento\|Cap. 18]] | ☐ |
| Crear usuarios y otorgar permisos | [[bd19_dcl\|Cap. 19]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| `WHERE` | `HAVING` | Filtra filas vs. grupos |
| `COUNT(*)` | `COUNT(col)` | Cuenta filas vs. valores no nulos |
| `INNER` | `LEFT` | Solo coincidencias vs. todas las de la izquierda |
| `DELETE` | `TRUNCATE` | Filas con condición y reversible vs. tabla vacía irreversible |
| `DROP` | `TRUNCATE` | Elimina estructura y datos vs. solo datos |
| `UNION` | `UNION ALL` | Elimina duplicados vs. los conserva |
| Subconsulta escalar | `EXISTS` | Devuelve un valor vs. verdadero/falso |
| `GRANT` | `REVOKE` | Otorga vs. quita |
| `VARCHAR` | `CHAR` | Longitud variable vs. fija |
| `DECIMAL` | `DOUBLE` | Exacto vs. aproximado |

## Ejercicio integrador del Módulo 3

> [!example] Enunciado (30 minutos)
> Sobre el esquema del municipio (`dispositivo`, `alerta`, `reparacion`, `tecnico`), escribí:
> 1. DDL de las cuatro tablas con PK, FK y dos `CHECK`.
> 2. Insertar 3 dispositivos, 5 alertas y 2 reparaciones.
> 3. Consulta: código y ubicación de los dispositivos con alertas de prioridad 1.
> 4. Consulta: cantidad de alertas por dispositivo, incluyendo los que tienen 0.
> 5. Consulta: costo total por técnico, solo los que superan $10.000.
> 6. Un usuario `reportes` con solo lectura.

> [!success]- Solución
> **1–2.**
> ```sql
> CREATE TABLE dispositivo (
>     id        INT AUTO_INCREMENT PRIMARY KEY,
>     codigo    VARCHAR(10) NOT NULL UNIQUE,
>     tipo      VARCHAR(20) NOT NULL,
>     ubicacion VARCHAR(100) NOT NULL,
>     CONSTRAINT ck_tipo CHECK (tipo IN ('semaforo','camara'))
> );
>
> CREATE TABLE alerta (
>     id             INT AUTO_INCREMENT PRIMARY KEY,
>     fecha          DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
>     mensaje        VARCHAR(200) NOT NULL,
>     prioridad      TINYINT NOT NULL,
>     atendida       BOOLEAN NOT NULL DEFAULT FALSE,
>     id_dispositivo INT NOT NULL,
>     CONSTRAINT ck_prio CHECK (prioridad BETWEEN 1 AND 5),
>     FOREIGN KEY (id_dispositivo) REFERENCES dispositivo(id) ON DELETE CASCADE
> );
>
> CREATE TABLE tecnico (
>     id        INT AUTO_INCREMENT PRIMARY KEY,
>     nombre    VARCHAR(60) NOT NULL,
>     matricula VARCHAR(20) NOT NULL UNIQUE
> );
>
> CREATE TABLE reparacion (
>     id         INT AUTO_INCREMENT PRIMARY KEY,
>     fecha      DATE NOT NULL,
>     costo      DECIMAL(10,2) NOT NULL DEFAULT 0,
>     id_alerta  INT NOT NULL UNIQUE,
>     id_tecnico INT NULL,
>     CONSTRAINT ck_costo CHECK (costo >= 0),
>     FOREIGN KEY (id_alerta) REFERENCES alerta(id) ON DELETE CASCADE,
>     FOREIGN KEY (id_tecnico) REFERENCES tecnico(id) ON DELETE SET NULL
> );
>
> INSERT INTO dispositivo (codigo, tipo, ubicacion) VALUES
>     ('S-01','semaforo','Belgrano'),
>     ('S-02','semaforo','San Martín'),
>     ('C-01','camara','Plaza');
>
> INSERT INTO alerta (mensaje, prioridad, id_dispositivo) VALUES
>     ('Lámpara', 2, 1),
>     ('Sin luz', 1, 2),
>     ('Offline', 1, 3),
>     ('Lente',   4, 3),
>     ('Suciedad',3, 1);
>
> INSERT INTO tecnico (nombre, matricula) VALUES ('Luis','M-01'), ('Eva','M-02');
>
> INSERT INTO reparacion (fecha, costo, id_alerta, id_tecnico) VALUES
>     ('2026-11-10', 15000, 1, 1),
>     ('2026-11-11', 5000,  2, 2);
> ```
> **3.**
> ```sql
> SELECT DISTINCT d.codigo, d.ubicacion
> FROM dispositivo d
> JOIN alerta a ON a.id_dispositivo = d.id
> WHERE a.prioridad = 1;
> ```
> **4.**
> ```sql
> SELECT d.codigo, COUNT(a.id) AS alertas
> FROM dispositivo d
> LEFT JOIN alerta a ON a.id_dispositivo = d.id
> GROUP BY d.codigo;
> ```
> **5.**
> ```sql
> SELECT t.nombre, SUM(r.costo) AS total
> FROM tecnico t
> JOIN reparacion r ON r.id_tecnico = t.id
> GROUP BY t.nombre
> HAVING SUM(r.costo) > 10000;
> ```
> **6.**
> ```sql
> CREATE USER 'reportes'@'localhost' IDENTIFIED BY 'Reportes2026!';
> GRANT SELECT ON municipio.* TO 'reportes'@'localhost';
> ```
>
> **Qué evalúa el tribunal:** que la FK esté en el lado N, que uses `LEFT JOIN` + `COUNT(a.id)` para el cero, que `HAVING` filtre el agregado y que el permiso sea mínimo.

## Oral del Módulo 3 (10 preguntas)

> [!question]- 1. ¿Por qué SQL es declarativo?
> Porque se describe el resultado deseado y el motor, mediante el optimizador, decide cómo obtenerlo.

> [!question]- 2. ¿Cuál es la diferencia entre DDL, DML y DCL?
> DDL define estructura; DML manipula datos; DCL controla el acceso.

> [!question]- 3. ¿Qué hace `ALTER TABLE`?
> Modifica la estructura: agrega, cambia o elimina columnas y restricciones.

> [!question]- 4. ¿Qué diferencia hay entre `DELETE` y `TRUNCATE`?
> `DELETE` borra filas con condición y puede revertirse; `TRUNCATE` vacía la tabla y no se revierte.

> [!question]- 5. ¿Por qué `WHERE col = NULL` no funciona?
> Porque `NULL` es desconocido: toda comparación da desconocido. Se usa `IS NULL`.

> [!question]- 6. `WHERE` vs. `HAVING`.
> `WHERE` filtra filas antes de agrupar; `HAVING` filtra grupos ya formados.

> [!question]- 7. `COUNT(*)` vs. `COUNT(columna)`.
> `COUNT(*)` cuenta filas; `COUNT(columna)` cuenta solo los valores no nulos.

> [!question]- 8. ¿Cuándo usás `LEFT JOIN`?
> Cuando querés conservar todas las filas de la izquierda aunque no tengan coincidencia, por ejemplo dispositivos sin alertas.

> [!question]- 9. ¿Qué es una subconsulta correlacionada?
> Una subconsulta que referencia una columna de la consulta externa y se evalúa por cada fila.

> [!question]- 10. ¿Qué es el principio de menor privilegio?
> Otorgar solo los permisos necesarios para la tarea, ni más ni por más tiempo.

## Lo que sigue

[[bd20_extensiones-procedimentales|20. Extensiones procedimentales de SQL]].

#libro2 #cierre #sql
