---
tags: [efip, base-de-datos, cierre]
libro: 2
parte: 4
---

# Cierre del Módulo 4 — Extensión procedimental

> [!info] Qué hacer con este archivo
> Verificación de PL/SQL. Si algo falla, volvé al capítulo.

## Checklist del Módulo 4

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Escribir un bloque con `DECLARE/BEGIN/EXCEPTION` | [[bd20_extensiones-procedimentales\|Cap. 20]] | ☐ |
| Usar `%TYPE` y `%ROWTYPE` | [[bd20_extensiones-procedimentales\|Cap. 20]] | ☐ |
| Escribir `IF`, `CASE`, `LOOP`, `FOR`, `WHILE` | [[bd20_extensiones-procedimentales\|Cap. 20]] | ☐ |
| Usar `SELECT INTO` y explicar sus excepciones | [[bd20_extensiones-procedimentales\|Cap. 20]] | ☐ |
| Crear procedimientos y funciones | [[bd21_programas-almacenados\|Cap. 21]] | ☐ |
| Diferenciar `IN`, `OUT`, `IN OUT` | [[bd21_programas-almacenados\|Cap. 21]] | ☐ |
| Recorrer con cursor explícito y con `FOR` | [[bd22_cursores\|Cap. 22]] | ☐ |
| Usar `SQL%ROWCOUNT` y `%NOTFOUND` | [[bd22_cursores\|Cap. 22]] | ☐ |
| Capturar excepciones predefinidas y propias | [[bd23_excepciones\|Cap. 23]] | ☐ |
| Crear un paquete con especificación y cuerpo | [[bd25_paquetes\|Cap. 25]] | ☐ |
| Crear un trigger de auditoría | [[bd24_triggers\|Cap. 24]] | ☐ |
| Explicar por qué un trigger puede ocultar lógica | [[bd24_triggers\|Cap. 24]] | ☐ |
| Traducir todo a MySQL | todos | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| SQL | PL/SQL | Declarativo vs. procedural |
| Bloque anónimo | Procedimiento | No se almacena vs. queda en la base |
| Procedimiento | Función | No devuelve vs. siempre devuelve |
| `IN` | `OUT` | Solo entrada vs. solo salida |
| Cursor implícito | Explícito | Automático vs. declarado con nombre |
| `%TYPE` | `%ROWTYPE` | Tipo de una columna vs. fila completa |
| Excepción predefinida | Definida por el usuario | La conoce Oracle vs. la declara el programador |
| `RAISE` | `RAISE_APPLICATION_ERROR` | Lanza una excepción declarada vs. lanza un error con código y mensaje |
| Trigger `BEFORE` | `AFTER` | Antes de aplicar el cambio vs. después |
| `:NEW` | `:OLD` | Valores nuevos vs. anteriores |

## Ejercicio integrador del Módulo 4

> [!example] Enunciado (30 minutos)
> Sobre el esquema del municipio, automatizá lo siguiente:
> 1. Un procedimiento `registrar_alerta(p_dispositivo, p_mensaje, p_prioridad)` que valide la prioridad y la inserte.
> 2. Una función `costo_total(p_dispositivo)` que devuelva la suma de reparaciones.
> 3. Un trigger que audite los cambios de prioridad en una tabla `auditoria_alerta`.
> 4. Un bloque anónimo que registre una alerta y muestre el costo total del dispositivo.

> [!success]- Solución
> **1. Procedimiento**
> ```sql
> CREATE OR REPLACE PROCEDURE registrar_alerta (
>     p_dispositivo IN NUMBER,
>     p_mensaje     IN VARCHAR2,
>     p_prioridad   IN NUMBER
> ) AS
> BEGIN
>     IF p_prioridad < 1 OR p_prioridad > 5 THEN
>         RAISE_APPLICATION_ERROR(-20001, 'Prioridad inválida');
>     END IF;
>
>     INSERT INTO alerta (mensaje, prioridad, id_dispositivo)
>     VALUES (p_mensaje, p_prioridad, p_dispositivo);
> END;
> /
> ```
> **2. Función**
> ```sql
> CREATE OR REPLACE FUNCTION costo_total (
>     p_dispositivo IN NUMBER
> ) RETURN NUMBER IS
>     v NUMBER;
> BEGIN
>     SELECT NVL(SUM(r.costo), 0)
>       INTO v
>       FROM alerta a
>       JOIN reparacion r ON r.id_alerta = a.id
>      WHERE a.id_dispositivo = p_dispositivo;
>     RETURN v;
> END;
> /
> ```
> **3. Trigger**
> ```sql
> CREATE OR REPLACE TRIGGER trg_alerta_aud
> AFTER UPDATE OF prioridad ON alerta
> FOR EACH ROW
> BEGIN
>     INSERT INTO auditoria_alerta
>         (id_alerta, prioridad_old, prioridad_new, usuario, fecha)
>     VALUES
>         (:OLD.id, :OLD.prioridad, :NEW.prioridad, USER, SYSDATE);
> END;
> /
> ```
> **4. Bloque**
> ```sql
> SET SERVEROUTPUT ON;
> BEGIN
>     registrar_alerta(1, 'Prueba', 2);
>     DBMS_OUTPUT.PUT_LINE('Costo total: ' || costo_total(1));
> END;
> /
> ```
>
> **Qué evalúa el tribunal:** que la validación esté antes del `INSERT`, que la función use `NVL` para no devolver `NULL`, que el trigger use `:OLD`/`:NEW` y que el bloque no mezcle sintaxis de MySQL.

## Oral del Módulo 4 (10 preguntas)

> [!question]- 1. ¿Qué es PL/SQL?
> La extensión procedural de SQL creada por Oracle, organizada en bloques con variables, control de flujo, cursores y excepciones.

> [!question]- 2. ¿Cuáles son las secciones de un bloque?
> `DECLARE` (opcional), `BEGIN ... END` (obligatoria) y `EXCEPTION` (opcional).

> [!question]- 3. ¿Qué diferencia hay entre bloque anónimo y procedimiento?
> El bloque anónimo no tiene nombre ni se almacena: se compila y ejecuta en cada llamada. El procedimiento queda guardado y se invoca por nombre.

> [!question]- 4. ¿Procedimiento o función?
> Función si necesito un valor para usar en una expresión; procedimiento si necesito ejecutar una acción.

> [!question]- 5. ¿Qué hace `%ROWTYPE`?
> Declara una variable con la estructura completa de una fila de la tabla indicada.

> [!question]- 6. ¿Qué es un cursor implícito?
> El área de trabajo que Oracle abre automáticamente para cada DML; se consulta con `SQL%ROWCOUNT`, `SQL%FOUND`, `SQL%NOTFOUND`.

> [!question]- 7. ¿Cuál es el ciclo de un cursor explícito?
> `OPEN`, `FETCH` repetido hasta `%NOTFOUND`, `CLOSE`.

> [!question]- 8. ¿Qué diferencia hay entre `NO_DATA_FOUND` y `TOO_MANY_ROWS`?
> El primero ocurre cuando el `SELECT INTO` no devuelve filas; el segundo, cuando devuelve más de una.

> [!question]- 9. ¿Para qué sirve `WHEN OTHERS`?
> Para capturar errores no tratados previamente. Debe ir al final y no debe silenciar el error: hay que registrar y, si corresponde, relanzar.

> [!question]- 10. ¿Cuándo usarías un trigger?
> Para auditoría, integridad técnica o acciones automáticas pequeñas y documentadas; no para reglas centrales del negocio.

## Fin del libro

> [!success] Terminaste el Libro 2
> Cubriste el Módulo 3 del EFIP: **5.1** modelo relacional, **5.2** diseño y normalización, **5.3** SQL y **5.4** extensión procedimental.
>
> Continuá con el [[bd_D_Mapa|mapa del programa]], el [[bd_B_Banco_preguntas|banco de preguntas]] y el [[bd_A_SQL_para_papel|SQL listo para papel]].

#libro2 #cierre #plsql
