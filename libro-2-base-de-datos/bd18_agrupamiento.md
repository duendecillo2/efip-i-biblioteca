---
tags: [efip, base-de-datos, agrupamiento]
libro: 2
capitulo: 18
subeje: "5.3"
---

# 18. Agrupamiento y funciones de grupo

> [!info] Al terminar este capítulo tenés que poder
> - Usar `COUNT`, `SUM`, `AVG`, `MIN` y `MAX`.
> - Diferenciar `COUNT(*)`, `COUNT(columna)` y `COUNT(DISTINCT ...)`.
> - Explicar `WHERE` vs. `HAVING`.
> - Agrupar por una o varias columnas.

> [!abstract] Qué debés saber (nivel 1)
> - Las funciones de grupo resumen **muchas filas en una**.
> - `GROUP BY` forma grupos; cada grupo devuelve una fila.
> - `WHERE` filtra **filas** antes de agrupar; `HAVING` filtra **grupos** después.
> - En el `SELECT` solo pueden ir columnas agrupadas y funciones de grupo.
> - `COUNT(*)` cuenta filas; `COUNT(col)` ignora `NULL`.
> - Los agregados ignoran `NULL`, salvo `COUNT(*)`.

## 18.1 Funciones de grupo

| Función | Qué devuelve | Ignora `NULL` |
|---|---|---|
| `COUNT(*)` | Cantidad de filas | No (cuenta todo) |
| `COUNT(col)` | Cantidad de valores no nulos | Sí |
| `COUNT(DISTINCT col)` | Cantidad de valores distintos no nulos | Sí |
| `SUM(col)` | Suma | Sí |
| `AVG(col)` | Promedio | Sí |
| `MIN(col)` | Mínimo | Sí |
| `MAX(col)` | Máximo | Sí |

```sql
SELECT COUNT(*) AS total_alertas,
       COUNT(id_tecnico) AS con_tecnico,
       COUNT(DISTINCT id_alerta) AS alertas_distintas
FROM reparacion;
```

> [!warning] `COUNT(*)` vs. `COUNT(columna)`
> Si hay 10 reparaciones y 3 sin técnico:
> - `COUNT(*)` = 10.
> - `COUNT(id_tecnico)` = 7.
> Es la pregunta clásica para ver si entendiste `NULL`.

## 18.2 `GROUP BY`

```sql
SELECT id_dispositivo, COUNT(*) AS alertas
FROM alerta
GROUP BY id_dispositivo;
```

| id_dispositivo | alertas |
|---:|---:|
| 1 | 3 |
| 2 | 1 |
| 3 | 5 |

### Regla de oro

> [!important] Todo lo que está en el `SELECT` debe estar agrupado o dentro de un agregado
> ```sql
> SELECT id_dispositivo, mensaje, COUNT(*)   -- MAL: mensaje no está agrupado
> FROM alerta GROUP BY id_dispositivo;
> ```
> MySQL con `ONLY_FULL_GROUP_BY` (por defecto en 8.0) lo rechaza. Es correcto que lo rechace: ¿qué mensaje mostrarías si hay 5?

### Agrupar por varias columnas

```sql
SELECT id_dispositivo, prioridad, COUNT(*) AS cantidad
FROM alerta
GROUP BY id_dispositivo, prioridad
ORDER BY id_dispositivo, prioridad;
```

Cada combinación `(dispositivo, prioridad)` es un grupo.

### Agrupar con `JOIN`

```sql
SELECT d.codigo, COUNT(a.id) AS alertas
FROM dispositivo d
LEFT JOIN alerta a ON a.id_dispositivo = d.id
GROUP BY d.codigo
ORDER BY alertas DESC;
```

> [!tip] `LEFT JOIN` + `COUNT(a.id)`
> Devuelve `0` para los dispositivos sin alertas. Si usás `COUNT(*)`, devuelve `1` (cuenta la fila del `LEFT` con `NULL`). **Contá la columna, no la fila.**

## 18.3 `WHERE` vs. `HAVING`

```mermaid
flowchart LR
    F["FROM"] --> W["WHERE<br/>filtra filas"] --> G["GROUP BY"] --> H["HAVING<br/>filtra grupos"] --> S["SELECT"]
```

```sql
-- Filtrar filas antes de agrupar
SELECT id_dispositivo, COUNT(*) AS criticas
FROM alerta
WHERE prioridad = 1
GROUP BY id_dispositivo;

-- Filtrar grupos después
SELECT id_dispositivo, COUNT(*) AS total
FROM alerta
GROUP BY id_dispositivo
HAVING COUNT(*) > 2;

-- Los dos
SELECT id_dispositivo, COUNT(*) AS criticas
FROM alerta
WHERE prioridad = 1
GROUP BY id_dispositivo
HAVING COUNT(*) >= 2;
```

> [!important] Criterio
> - La condición depende de **una fila** → `WHERE`.
> - La condición depende de **un agregado** → `HAVING`.
> - Si podés usar `WHERE`, usalo: filtra antes y trabaja con menos datos.

## 18.4 `NULL` en agregados

| Consulta | Resultado con valores `10, NULL, 20` |
|---|---|
| `SUM(x)` | `30` |
| `AVG(x)` | `15` (divide por 2, no por 3) |
| `COUNT(*)` | `3` |
| `COUNT(x)` | `2` |
| `MIN(x)` / `MAX(x)` | `10` / `20` |

> [!warning] El promedio que sorprende
> `AVG` divide por la cantidad de valores **no nulos**. Si querés que los nulos cuenten como cero: `AVG(COALESCE(x, 0))`.

## 18.5 Programa completo

```sql
-- 1. Alertas por dispositivo, incluyendo los que no tienen
SELECT d.codigo,
       d.tipo,
       COUNT(a.id) AS alertas,
       IFNULL(MAX(a.prioridad), 0) AS prioridad_max
FROM dispositivo d
LEFT JOIN alerta a ON a.id_dispositivo = d.id
GROUP BY d.codigo, d.tipo
ORDER BY alertas DESC, d.codigo;

-- 2. Dispositivos con más de 2 alertas
SELECT d.codigo, COUNT(*) AS total
FROM dispositivo d
JOIN alerta a ON a.id_dispositivo = d.id
GROUP BY d.codigo
HAVING COUNT(*) > 2;

-- 3. Costo total y promedio por técnico
SELECT t.nombre,
       COUNT(r.id) AS reparaciones,
       SUM(r.costo) AS total,
       ROUND(AVG(r.costo), 2) AS promedio
FROM tecnico t
LEFT JOIN reparacion r ON r.id_tecnico = t.id
GROUP BY t.nombre
ORDER BY total DESC;

-- 4. Alertas por mes
SELECT YEAR(fecha) AS anio,
       MONTH(fecha) AS mes,
       COUNT(*) AS alertas
FROM alerta
GROUP BY YEAR(fecha), MONTH(fecha)
ORDER BY anio, mes;
```

Salida del punto 1 (ejemplo):

```text
+--------+----------+---------+---------------+
| codigo | tipo     | alertas | prioridad_max |
+--------+----------+---------+---------------+
| C-01   | camara   |       5 |             1 |
| S-01   | semaforo |       3 |             2 |
| S-02   | semaforo |       0 |             0 |
+--------+----------+---------+---------------+
```

## Cómo trazar una agrupación

Tabla `alerta`:

| id | id_dispositivo | prioridad |
|---:|---:|---:|
| 1 | 1 | 2 |
| 2 | 1 | 1 |
| 3 | 2 | 4 |
| 4 | 1 | 1 |

```sql
SELECT id_dispositivo, COUNT(*) AS total
FROM alerta
WHERE prioridad <= 2
GROUP BY id_dispositivo
HAVING COUNT(*) >= 2;
```

| Paso | Resultado |
|---|---|
| `WHERE` | filas 1, 2 y 4 |
| `GROUP BY` | dispositivo 1: 3 filas; dispositivo 2: 0 |
| `HAVING` | solo dispositivo 1 (3 ≥ 2) |
| Resultado | `(1, 3)` |

## Errores que suelen tomar

| Error | Corrección |
|---|---|
| Columna no agrupada en `SELECT` | Agregarla al `GROUP BY` o envolverla en un agregado |
| Filtrar agregados con `WHERE` | Usar `HAVING` |
| `COUNT(*)` esperando ignorar nulos | `COUNT(columna)` |
| `AVG` con nulos esperando dividir por n | `AVG(COALESCE(col, 0))` |
| `GROUP BY` por el alias | Usar el nombre o la expresión |
| Agrupar de más | Resultado con filas repetidas |

## Ejercicios

> [!example]- 1. Básico
> **Enunciado:** cantidad total de alertas y cantidad de prioridad 1.
> **Solución:**
> ```sql
> SELECT COUNT(*) AS total,
>        SUM(prioridad = 1) AS criticas
> FROM alerta;
> ```

> [!example]- 2. Por grupo
> **Enunciado:** cantidad de dispositivos por tipo.
> **Solución:**
> ```sql
> SELECT tipo, COUNT(*) AS cantidad
> FROM dispositivo
> GROUP BY tipo;
> ```

> [!example]- 3. `HAVING`
> **Enunciado:** técnicos con más de 3 reparaciones.
> **Solución:**
> ```sql
> SELECT id_tecnico, COUNT(*) AS total
> FROM reparacion
> GROUP BY id_tecnico
> HAVING COUNT(*) > 3;
> ```

> [!example]- 4. Promedio
> **Enunciado:** costo promedio de reparación por mes.
> **Solución:**
> ```sql
> SELECT YEAR(fecha) AS anio, MONTH(fecha) AS mes,
>        ROUND(AVG(costo), 2) AS promedio
> FROM reparacion
> GROUP BY anio, mes
> ORDER BY anio, mes;
> ```

> [!example]- 5. a papel
> **Enunciado:** código de dispositivo y cantidad de alertas críticas (prioridad 1), solo para los que tienen al menos 2.
> **Solución:**
> ```sql
> SELECT d.codigo, COUNT(*) AS criticas
> FROM dispositivo d
> JOIN alerta a ON a.id_dispositivo = d.id
> WHERE a.prioridad = 1
> GROUP BY d.codigo
> HAVING COUNT(*) >= 2;
> ```

## Lo que sigue

[[bd19_dcl|19. DCL: permisos y roles]].

#libro2 #basededatos #agrupamiento
