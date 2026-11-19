---
tags: [efip, base-de-datos, anexo, errores]
libro: 2
anexo: C
---

# C. Errores frecuentes — Base de Datos

> [!info] Cómo usarlo
> Antes de un simulacro, leé solo esta lista. Después, marcá los que cometiste.

## C.1 Errores de modelado

| Error | Corrección |
|---|---|
| Guardar varios valores en una columna | Tabla aparte (1FN) |
| Columnas `telefono1`, `telefono2`, `telefono3` | Tabla de teléfonos |
| FK en el lado “1” de una 1:N | Va en el lado “N” |
| M:N sin tabla puente | Tabla intermedia con PK compuesta |
| 1:1 sin `UNIQUE` | Se convierte en 1:N |
| Usar un dato mutable como PK | Elegir uno estable |
| Entidad débil con PK simple | PK compuesta (identificadora + parcial) |
| Guardar un atributo derivado sin necesidad | Calcularlo |

## C.2 Errores de normalización

| Error | Corrección |
|---|---|
| Creer que 1FN es “tener PK” | Es atomicidad |
| Aplicar 2FN con PK simple | No aporta |
| Confundir dependencia parcial con transitiva | Parcial = parte de la clave; transitiva = otro no clave |
| Separar el precio histórico de la venta | Es un hecho de la línea |
| Normalizar y perder la FK | Verificar el join inverso |
| Desnormalizar sin justificar | No se acepta |

## C.3 Errores de SQL

| Error | Mensaje / consecuencia | Corrección |
|---|---|---|
| `WHERE col = NULL` | No devuelve filas | `IS NULL` |
| `UPDATE` sin `WHERE` | Modifica todo | Verificar con `SELECT` |
| `DELETE` sin `WHERE` | Vacía la tabla | Idem |
| `SELECT *` en producción | Columnas de más | Nombrar columnas |
| Alias en `WHERE` | `Unknown column` | Usar la expresión |
| `GROUP BY` incompleto | `ONLY_FULL_GROUP_BY` | Agrupar o agregar |
| `HAVING` para filas | Resultado incorrecto | Usar `WHERE` |
| `COUNT(*)` esperando ignorar nulos | Cuenta de más | `COUNT(col)` |
| `AVG` con nulos | Divide por menos | `COALESCE` |
| Olvidar `ON` en join | Producto cartesiano | `JOIN ... ON` |
| `INNER` donde hacía falta `LEFT` | Se pierden filas | `LEFT JOIN` |
| Filtrar la tabla derecha en `WHERE` de un `LEFT` | Se vuelve `INNER` | Condición en el `ON` |
| `NOT IN` con `NULL` | Resultado vacío | `NOT EXISTS` |
| `LIMIT` sin `ORDER BY` | Orden impredecible | Ordenar primero |
| `LIKE '%x'` esperando índice | Escaneo completo | Prefijo fijo |
| `DROP` creyendo que solo borra datos | Se pierde la tabla | `TRUNCATE` o `DELETE` |

## C.4 Errores de DDL

| Error | Mensaje | Corrección |
|---|---|---|
| Crear FK antes que el padre | `ERROR 1824` | Crear el padre primero |
| Tipos distintos en FK y PK | `ERROR 3780` | Mismo tipo y signo |
| `CHECK` ignorado | MySQL < 8.0.16 | Actualizar versión |
| `VARCHAR` sin longitud | Error de sintaxis | `VARCHAR(n)` |
| `utf8` en lugar de `utf8mb4` | No guarda emojis | `utf8mb4` |
| `MODIFY` a un tipo más corto | Trunca datos | Verificar longitudes |

## C.5 Errores de PL/SQL

| Error | Corrección |
|---|---|
| `=` para asignar | `:=` |
| Concatenar con `+` | `||` |
| Olvidar `SET SERVEROUTPUT ON` | Agregarlo |
| `SELECT` sin `INTO` dentro del bloque | `SELECT ... INTO` |
| Declarar variables después de `BEGIN` | En `DECLARE` |
| Olvidar `/` al final | Agregarlo |
| `WHEN OTHERS` primero | Va último |
| `WHEN OTHERS` vacío | Registrar y relanzar |
| Código de error fuera de `-20000..-20999` | Rango válido |
| `:NEW` en `DELETE` | Solo `:OLD` |
| Trigger sin `FOR EACH ROW` | Se ejecuta por sentencia |
| Cursor sin `CLOSE` | Cerrar o usar `FOR` |
| `EXIT WHEN` antes del `FETCH` | Evaluar después |

## C.6 Errores de permisos

| Error | Corrección |
|---|---|
| Crear usuario y esperar que lea | Otorgar `SELECT` |
| `GRANT ... ON tabla` sin base | `base.tabla` |
| `REVOKE` esperando borrar el usuario | `DROP USER` |
| `'user'@'%'` sin necesidad | Restringir host |
| `ALL PRIVILEGES` a todos | Menor privilegio |
| `WITH GRANT OPTION` sin control | Evitarlo |

## C.7 Checklist de 60 segundos

- [ ] ¿La FK está en el lado N?
- [ ] ¿La tabla está en 1FN? ¿Hay listas en una celda?
- [ ] ¿La PK es única y no nula?
- [ ] ¿Usé `IS NULL` y no `= NULL`?
- [ ] ¿El `GROUP BY` incluye todo lo que no es agregado?
- [ ] ¿`WHERE` filtra filas y `HAVING` grupos?
- [ ] ¿El `JOIN` tiene `ON`?
- [ ] ¿Usé `LEFT JOIN` donde podía faltar el par?
- [ ] ¿`COUNT(col)` en lugar de `COUNT(*)` para contar no nulos?
- [ ] ¿El `UPDATE`/`DELETE` tiene `WHERE`?
- [ ] ¿El bloque PL/SQL usa `:=` y tiene `/` al final?
- [ ] ¿`WHEN OTHERS` está al final?

#libro2 #anexo #errores
