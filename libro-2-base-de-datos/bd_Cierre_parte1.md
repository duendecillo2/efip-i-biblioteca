---
tags: [efip, base-de-datos, cierre]
libro: 2
parte: 1
---

# Cierre del Módulo 1 — Motores y modelo relacional

> [!info] Qué hacer con este archivo
> Verificación, no contenido nuevo. Si fallás en algo, volvé al capítulo antes de seguir.

## Checklist del Módulo 1

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Diferenciar base de datos, SGBD y motor | [[bd01_motores-de-bd\|Cap. 1]] | ☐ |
| Explicar cliente-servidor y el rol del optimizador | [[bd01_motores-de-bd\|Cap. 1]] | ☐ |
| Describir las capas de una aplicación en BD | [[bd02_aplicacion-en-bd\|Cap. 2]] | ☐ |
| Diferenciar servidor, instancia, esquema y catálogo | [[bd02_aplicacion-en-bd\|Cap. 2]] | ☐ |
| Asignar permisos con menor privilegio | [[bd02_aplicacion-en-bd\|Cap. 2]] | ☐ |
| Consultar el diccionario de datos | [[bd02_aplicacion-en-bd\|Cap. 2]] | ☐ |
| Ubicar Oracle, MySQL y SQLite | [[bd01_motores-de-bd\|Cap. 1]] | ☐ |
| Nombrar cada componente de una relación | [[bd03_componentes-modelo-relacional\|Cap. 3]] | ☐ |
| Calcular grado y cardinalidad | [[bd03_componentes-modelo-relacional\|Cap. 3]] | ☐ |
| Elegir una clave primaria y justificarla | [[bd03_componentes-modelo-relacional\|Cap. 3]] | ☐ |
| Aplicar σ, π, ρ, ×, ∪, − | [[bd05_algebra-relacional\|Cap. 5]] | ☐ |
| Construir un join desde el producto | [[bd05_algebra-relacional\|Cap. 5]] | ☐ |
| Usar join natural, división, asignación y agregación | [[bd05_algebra-relacional\|Cap. 5]] | ☐ |
| Expresar “todos” con división | [[bd05_algebra-relacional\|Cap. 5]] | ☐ |
| Explicar las reglas de Codd y el diccionario | [[bd03_componentes-modelo-relacional\|Cap. 3]] | ☐ |
| Escribir PK, FK, `UNIQUE`, `CHECK` | [[bd04_claves-e-integridad\|Cap. 4]] | ☐ |
| Elegir la acción referencial correcta | [[bd04_claves-e-integridad\|Cap. 4]] | ☐ |
| Reconocer errores 1062, 1451, 1452, 3819 | [[bd04_claves-e-integridad\|Cap. 4]] | ☐ |

## Tabla de diferencias

| A | B | Diferencia central |
|---|---|---|
| Base de datos | SGBD | Datos vs. software que los administra |
| Relación | Tabla | Concepto formal vs. implementación (que puede repetir filas) |
| Grado | Cardinalidad | Columnas vs. filas |
| Clave candidata | Clave primaria | Todas las que identifican vs. la elegida |
| PK | `UNIQUE` | No nula y una sola vs. admite `NULL` y varias |
| `σ` | `π` | Filtra filas vs. elige columnas |
| `×` | Join | Todas las combinaciones vs. solo las que cumplen la igualdad |
| `RESTRICT` | `CASCADE` | Impide borrar vs. borra en cascada |

## Ejercicio integrador del Módulo 1

> [!example] Enunciado (25 minutos)
> El municipio tiene dispositivos (semáforos y cámaras) y alertas. Se pide:
> 1. Identificar entidades, atributos y claves.
> 2. Escribir el DDL con PK, FK y dos `CHECK`.
> 3. Expresar en álgebra: “código de los dispositivos que tienen alertas de prioridad 1”.
> 4. Escribir el SQL equivalente.

> [!success]- Solución
> **1. Modelo**
>
> | Entidad | Atributos | PK |
> |---|---|---|
> | `dispositivo` | id, codigo, tipo, ubicacion, activo | `id` |
> | `alerta` | id, mensaje, prioridad, fecha, id_dispositivo | `id` |
>
> **2. DDL**
> ```sql
> CREATE TABLE dispositivo (
>     id        INT AUTO_INCREMENT PRIMARY KEY,
>     codigo    VARCHAR(10) NOT NULL UNIQUE,
>     tipo      VARCHAR(20) NOT NULL,
>     ubicacion VARCHAR(100) NOT NULL,
>     activo    BOOLEAN NOT NULL DEFAULT TRUE,
>     CONSTRAINT ck_tipo CHECK (tipo IN ('semaforo','camara'))
> );
>
> CREATE TABLE alerta (
>     id             INT AUTO_INCREMENT PRIMARY KEY,
>     mensaje        VARCHAR(200) NOT NULL,
>     prioridad      TINYINT NOT NULL,
>     atendida       BOOLEAN NOT NULL DEFAULT FALSE,
>     fecha          DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
>     id_dispositivo INT NOT NULL,
>     CONSTRAINT ck_prioridad CHECK (prioridad BETWEEN 1 AND 5),
>     CONSTRAINT fk_alerta_disp FOREIGN KEY (id_dispositivo)
>         REFERENCES dispositivo(id) ON DELETE CASCADE
> );
> ```
> **3. Álgebra**
> ```text
> π codigo ( σ prioridad = 1 ( DISPOSITIVO ⋈ ALERTA ) )
> ```
> **4. SQL**
> ```sql
> SELECT DISTINCT d.codigo
> FROM dispositivo d
> JOIN alerta a ON a.id_dispositivo = d.id
> WHERE a.prioridad = 1;
> ```
>
> **Qué evalúa el tribunal:** que la FK esté en el lado N, que el `CHECK` limite valores, que el join use la clave y que la proyección no repita códigos.

## Oral del Módulo 1 (8 preguntas)

> [!question]- 1. ¿Qué es una base de datos?
> Conjunto de datos estructurados y definidos por un proceso, que evita redundancia y se almacena en un medio masivo.

> [!question]- 2. ¿Qué diferencia hay entre grado y cardinalidad?
> El grado es la cantidad de columnas; la cardinalidad, la cantidad de filas.

> [!question]- 3. ¿Qué es un dominio?
> El conjunto de valores permitidos para un atributo.

> [!question]- 4. ¿Qué es una clave candidata?
> Un conjunto de atributos que identifica de forma única cada fila. La primaria es la candidata elegida.

> [!question]- 5. ¿Por qué conviene una clave estable?
> Porque si cambia, hay que actualizar todas las referencias; se rompe la integridad y se complica el mantenimiento.

> [!question]- 6. ¿Qué diferencia hay entre `σ` y `π`?
> `σ` filtra filas por una condición; `π` elige columnas y elimina duplicados.

> [!question]- 7. ¿Qué es el join en álgebra relacional?
> Una selección sobre el producto cartesiano, con la condición de igualdad entre claves.

> [!question]- 8. ¿Qué es la integridad referencial?
> La garantía de que toda clave foránea referencia una fila existente (o es nula si la relación es opcional).

## Lo que sigue

[[bd06_analisis-y-diseno|6. Análisis y diseño de un modelo de datos]].

#libro2 #cierre #basededatos
