---
tags: [efip, base-de-datos, anexo, oral]
libro: 2
anexo: B
---

# B. Banco de preguntas de oral — Base de Datos

> [!info] Cómo usarlo
> Tapá la respuesta, contestá en voz alta y recién después abrí. Aplicá la regla del EFIP: definir → cómo funciona → operaciones → aplicar → justificar.

## 5.1 Modelo relacional

> [!question]- 1. ¿Qué es una base de datos?
> Conjunto de datos estructurados y definidos por un proceso, que evita redundancia y se almacena en un medio masivo.

> [!question]- 2. ¿Qué diferencia hay entre base de datos y SGBD?
> La base son los datos; el SGBD es el software que los define, almacena, consulta y controla.

> [!question]- 3. ¿Qué es una relación?
> Una representación bidimensional de filas (tuplas) y columnas (atributos); el concepto primitivo del modelo relacional.

> [!question]- 4. Grado y cardinalidad.
> Grado = cantidad de columnas. Cardinalidad = cantidad de filas.

> [!question]- 5. ¿Qué es un dominio?
> El conjunto de valores permitidos para un atributo.

> [!question]- 6. ¿Qué diferencia hay entre cabecera y cuerpo?
> La cabecera es el conjunto de atributos; el cuerpo, el conjunto de tuplas.

> [!question]- 7. ¿Qué es una clave candidata?
> Un conjunto de atributos que identifica de forma única cada fila.

> [!question]- 8. ¿Cómo elegís la clave primaria?
> Debe ser única, no nula, estable, simple si es posible y corta.

> [!question]- 9. ¿Por qué no usar la dirección como clave?
> Porque cambia: obligaría a actualizar todas las referencias y rompería la integridad.

> [!question]- 10. ¿Qué es la integridad referencial?
> Que toda clave foránea referencie una fila existente o sea nula si la relación es opcional.

> [!question]- 11. ¿Qué hace `σ`?
> Selecciona las filas que cumplen una condición.

> [!question]- 12. ¿Qué hace `π` y qué pasa con los duplicados?
> Proyecta columnas y **elimina** duplicados, porque el resultado es un conjunto.

> [!question]- 13. ¿Qué es el producto cartesiano?
> La combinación de cada fila de una relación con cada fila de otra; su cardinalidad es el producto.

> [!question]- 14. ¿Qué es un join en álgebra relacional?
> Una selección sobre el producto cartesiano con la condición de igualdad entre claves.

> [!question]- 15. ¿Por qué el álgebra relacional importa?
> Es el fundamento formal de SQL y la base del optimizador de consultas.

## 5.2 Diseño y normalización

> [!question]- 16. ¿Qué es una entidad?
> Una clase de objetos del mundo real distinguibles entre sí; se representa como tabla.

> [!question]- 17. ¿Cómo distinguís entidad de atributo?
> Si tiene identidad y datos propios, es entidad; si solo describe a otra, es atributo.

> [!question]- 18. Tipos de atributo.
> Simple, compuesto, monovalorado, multivalorado, derivado y clave.

> [!question]- 19. ¿Qué significa un `NULL`?
> Que el valor no aplica, es desconocido o se perdió. No es cero ni cadena vacía.

> [!question]- 20. Cardinalidades posibles.
> 1:1, 1:M y M:N.

> [!question]- 21. ¿Dónde va la FK en una 1:N?
> En el lado “muchos”.

> [!question]- 22. ¿Cómo se implementa una M:N?
> Con una tabla puente cuya PK es la combinación de las dos FK.

> [!question]- 23. ¿Qué es una entidad débil?
> Una entidad sin clave propia, identificada por otra entidad más una clave parcial.

> [!question]- 24. ¿Qué es la normalización?
> Técnica para diseñar la estructura lógica de los datos evitando redundancia y anomalías.

> [!question]- 25. ¿Qué exige la 1FN?
> Valores atómicos: sin grupos repetitivos ni listas en una celda.

> [!question]- 26. ¿Cuándo importa la 2FN?
> Cuando la clave primaria es compuesta: todo atributo no clave debe depender de la clave completa.

> [!question]- 27. ¿Qué es una dependencia transitiva?
> `A → B` y `B → C` con B no clave. Viola 3FN.

> [!question]- 28. Nombrá las tres anomalías.
> Inserción, modificación y borrado.

> [!question]- 29. ¿Qué es BCFN?
> Una forma más estricta que 3FN: todo determinante es una clave candidata.

> [!question]- 30. ¿Desnormalizarías?
> Solo con una razón medida (rendimiento) y documentando cómo se mantiene la consistencia.

## 5.3 SQL

> [!question]- 31. ¿Por qué SQL es declarativo?
> Porque se describe el resultado y el optimizador decide el procedimiento de acceso.

> [!question]- 32. DDL, DML y DCL.
> DDL define estructura (`CREATE`, `ALTER`, `DROP`); DML manipula datos (`SELECT`, `INSERT`, `UPDATE`, `DELETE`); DCL controla acceso (`GRANT`, `REVOKE`).

> [!question]- 33. Orden lógico de una consulta.
> `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT`.

> [!question]- 34. `CHAR` vs. `VARCHAR`.
> Longitud fija vs. variable.

> [!question]- 35. ¿Por qué `DECIMAL` para dinero?
> Porque es exacto; `DOUBLE` es aproximado.

> [!question]- 36. `DELETE`, `TRUNCATE` y `DROP`.
> Borra filas (reversible) / vacía la tabla (no reversible) / elimina la tabla.

> [!question]- 37. ¿Por qué `WHERE col = NULL` no funciona?
> Porque `NULL` es desconocido: la comparación da desconocido. Se usa `IS NULL`.

> [!question]- 38. `WHERE` vs. `HAVING`.
> Filtra filas antes de agrupar vs. filtra grupos ya formados.

> [!question]- 39. `COUNT(*)` vs. `COUNT(col)`.
> Cuenta filas vs. cuenta valores no nulos.

> [!question]- 40. `INNER` vs. `LEFT JOIN`.
> Solo coincidencias vs. todas las filas de la izquierda, con `NULL` donde no hay par.

> [!question]- 41. ¿Cómo encontrás registros sin relación?
> `LEFT JOIN ... WHERE derecha.id IS NULL` o `NOT EXISTS`.

> [!question]- 42. ¿Qué es una subconsulta correlacionada?
> Una que referencia una columna de la consulta externa y se evalúa por cada fila.

> [!question]- 43. ¿Qué hace `DISTINCT`?
> Elimina filas duplicadas del resultado.

> [!question]- 44. ¿Qué es un índice y cuándo lo creás?
> Una estructura que acelera búsquedas por una columna; se crea en columnas usadas en `WHERE`, `JOIN` u `ORDER BY` con buena selectividad.

> [!question]- 45. ¿Qué es el principio de menor privilegio?
> Otorgar solo los permisos necesarios, ni más ni por más tiempo.

## 5.4 Extensión procedimental

> [!question]- 46. ¿Qué es PL/SQL?
> La extensión procedural de SQL de Oracle, organizada en bloques con variables, control de flujo, cursores y excepciones.

> [!question]- 47. Secciones de un bloque.
> `DECLARE` (opcional), `BEGIN ... END` (obligatoria), `EXCEPTION` (opcional).

> [!question]- 48. Bloque anónimo vs. procedimiento.
> El anónimo no se almacena y se compila en cada ejecución; el procedimiento queda guardado y se invoca por nombre.

> [!question]- 49. Procedimiento vs. función.
> La función siempre devuelve un valor; el procedimiento ejecuta una tarea y puede devolver por `OUT`.

> [!question]- 50. `IN`, `OUT`, `IN OUT`.
> Entrada, salida, y ambas.

> [!question]- 51. `%TYPE` y `%ROWTYPE`.
> Toman el tipo de una columna y la estructura completa de una fila, respectivamente.

> [!question]- 52. ¿Qué hace `SELECT INTO` y qué excepciones puede lanzar?
> Asigna una fila a variables; puede lanzar `NO_DATA_FOUND` o `TOO_MANY_ROWS`.

> [!question]- 53. Cursor implícito vs. explícito.
> El implícito lo abre Oracle para cada DML; el explícito se declara con nombre y se recorre con `OPEN/FETCH/CLOSE`.

> [!question]- 54. Atributos del cursor implícito.
> `SQL%ROWCOUNT`, `SQL%FOUND`, `SQL%NOTFOUND`, `SQL%ISOPEN`.

> [!question]- 55. ¿Cuándo usás cursor y cuándo SQL de conjunto?
> Cursor solo si la lógica depende fila a fila; si se puede resolver con una sentencia, se usa SQL.

> [!question]- 56. Excepciones predefinidas importantes.
> `NO_DATA_FOUND`, `TOO_MANY_ROWS`, `ZERO_DIVIDE`, `DUP_VAL_ON_INDEX`.

> [!question]- 57. `RAISE` vs. `RAISE_APPLICATION_ERROR`.
> Lanza una excepción declarada vs. lanza un error con código (`-20000..-20999`) y mensaje.

> [!question]- 58. ¿Por qué `WHEN OTHERS` va al final?
> Porque captura cualquier error no tratado antes; si va primero, los demás son inalcanzables.

> [!question]- 59. ¿Qué es un paquete?
> Un agrupamiento de procedimientos, funciones, variables y cursores, con especificación pública y cuerpo.

> [!question]- 60. ¿Qué es un trigger y cuándo lo usás?
> Código que se ejecuta automáticamente ante DML; se usa para auditoría e integridad técnica, no para reglas centrales.

> [!question]- 61. `:NEW` y `:OLD`.
> Valores nuevos y anteriores de la fila. En `DELETE` solo existe `:OLD`.

> [!question]- 62. Trigger de fila vs. de sentencia.
> `FOR EACH ROW` se ejecuta por fila afectada; sin él, una vez por sentencia.

## Preguntas integradoras

> [!question]- 63. Modelá dispositivos y alertas y justificá las claves.
> `dispositivo(id PK, codigo UNIQUE, tipo, ubicacion)` y `alerta(id PK, fecha, mensaje, prioridad, id_dispositivo FK)`. La FK va en alerta porque un dispositivo tiene muchas alertas.

> [!question]- 64. ¿Cómo evitás que se carguen alertas sin dispositivo?
> Con `id_dispositivo NOT NULL` y una FK que referencia `dispositivo(id)`.

> [!question]- 65. ¿Qué consulta usarías para el tablero de control?
> Un `LEFT JOIN` de dispositivo con alerta, `COUNT(a.id)` y `MAX(prioridad)`, agrupado por dispositivo.

#libro2 #anexo #oral
