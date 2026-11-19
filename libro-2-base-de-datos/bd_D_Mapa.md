---
tags: [efip, base-de-datos, anexo, mapa]
libro: 2
anexo: D
---

# D. Mapa del programa y trazabilidad — Base de Datos

> [!info] Para qué sirve
> Ver qué lectura oficial cubre cada capítulo, de dónde sale el contenido y qué quedó afuera.

## D.1 Cobertura por lectura oficial

Base: **INF387 — Base de Datos I**, 16 lecturas (`/home/jmcanguillen/Documents/siglo21/efip-1/base-de-datos/modulos`).

| Módulo | Lectura | Título oficial | Capítulo(s) |
|---|---|---|---|
| 1 | M1L1 | Motores de base de datos relacionales | [[bd01_motores-de-bd\|1]] |
| 1 | M1L2 | Componentes del motor de bases de datos MySQL | [[bd02_aplicacion-en-bd\|2]] |
| 1 | M1L3 | Componentes del modelo relacional en MySQL | [[bd03_componentes-modelo-relacional\|3]] · [[bd04_claves-e-integridad\|4]] |
| 1 | M1L4 | Álgebra relacional | [[bd05_algebra-relacional\|5]] |
| 2 | M2L1 | Análisis y diseño de un modelo de datos relacional | [[bd06_analisis-y-diseno\|6]] |
| 2 | M2L2 | Normalización de tablas de un modelo relacional | [[bd07_normalizacion-1fn-3fn\|7]] |
| 2 | M2L3 | Normalización más allá de la 1NF | [[bd08_normalizacion-casos\|8]] |
| 2 | M2L4 | Herramienta gráfica DER | [[bd09_der\|9]] · [[bd10_der-a-tablas\|10]] |
| 3 | M3L1 | El lenguaje SQL | [[bd11_lenguaje-sql\|11]] |
| 3 | M3L2 | Sentencias DML: INSERT, UPDATE y DELETE | [[bd12_dml\|12]] |
| 3 | M3L3 | Sentencias DDL: CREATE, ALTER y DROP | [[bd13_ddl\|13]] |
| 3 | M3L4 | Convenciones de nombres y tipos de datos | [[bd14_convenciones-y-tipos\|14]] |
| 4 | M4L1 | Las extensiones procedimentales de SQL | [[bd20_extensiones-procedimentales\|20]] |
| 4 | M4L2 | Programas almacenados en MySQL | [[bd21_programas-almacenados\|21]] |
| 4 | M4L3 | El uso de SQL en SQL/PSM | [[bd22_cursores\|22]] |
| 4 | M4L4 | Triggers o disparadores | [[bd24_triggers\|24]] |

### Complementos que pide el programa (5.3 y 5.4)

| Tema | Capítulo | Por qué no tiene lectura propia |
|---|---|---|
| SELECT, JOIN, subconsultas, agrupamiento | [[bd15_select\|15]] · [[bd16_joins-subconsultas\|16]] · [[bd17_metodo-consultas\|17]] · [[bd18_agrupamiento\|18]] | M3L2 incluye SELECT en la definición de DML, pero la lectura solo desarrolla INSERT/UPDATE/DELETE |
| DCL (usuarios, roles, privilegios) | [[bd19_dcl\|19]] | El programa 5.3 lo exige; la cátedra lo menciona en M1L2 y M3L1 sin desarrollarlo |
| Excepciones | [[bd23_excepciones\|23]] | M4L1 menciona el manejo de condiciones; el detalle es de PL/SQL |
| Paquetes | [[bd25_paquetes\|25]] | Oracle; MySQL no los tiene (se cubre el equivalente) |

## D.2 Cobertura por sub-eje del EFIP

| Sub-eje oficial | Capítulos | Estado |
|---|---|---|
| **5.1** Modelo relacional: introducción, componentes y reglas, álgebra, motor | [[bd01_motores-de-bd\|1]] · [[bd02_aplicacion-en-bd\|2]] · [[bd03_componentes-modelo-relacional\|3]] · [[bd04_claves-e-integridad\|4]] · [[bd05_algebra-relacional\|5]] | ✅ Completo |
| **5.2** Diseño: normalización, modelo entidad-relación | [[bd06_analisis-y-diseno\|6]] · [[bd07_normalizacion-1fn-3fn\|7]] · [[bd08_normalizacion-casos\|8]] · [[bd09_der\|9]] · [[bd10_der-a-tablas\|10]] | ✅ Completo |
| **5.3** SQL: DDL, DML, DCL, SELECT, estructuras | [[bd11_lenguaje-sql\|11]] · [[bd12_dml\|12]] · [[bd13_ddl\|13]] · [[bd14_convenciones-y-tipos\|14]] · [[bd15_select\|15]] · [[bd16_joins-subconsultas\|16]] · [[bd17_metodo-consultas\|17]] · [[bd18_agrupamiento\|18]] · [[bd19_dcl\|19]] | ✅ Completo |
| **5.4** Extensión procedimental | [[bd20_extensiones-procedimentales\|20]] · [[bd21_programas-almacenados\|21]] · [[bd22_cursores\|22]] · [[bd23_excepciones\|23]] · [[bd24_triggers\|24]] · [[bd25_paquetes\|25]] | ✅ Completo |

## D.3 Fuente de cada bloque

| Bloque | Base Siglo 21 | Complemento |
|---|---|---|
| 5.1 | M1L1–M1L4 (`modulos/m1l1.pdf` … `m1l4.pdf`) | **UTN**: `3) Modelo Relacional`, `5) Álgebra relacional` (división, agregación); UP M06/M07 |
| 5.2 | M2L1–M2L4 | **UTN**: `1) Modelo DER`, `3) normalización` + ejercicios resueltos; **UP** M03 (conversión); **UNLP** BD1 |
| 5.3 | M3L1–M3L4 | **UTN**: `4) SQL`, `Tips sobre SQL.pdf`; **UP** M08–M12; MySQL 8.0 |
| 5.4 | M4L1–M4L4 | **UP** Lab II, **UNLP** BD2, manual MySQL (SQL/PSM) |
| Anexo E | **Fuera del programa S21** | **UTN**: `6) Transacciones` |

> [!important] La base manda
> Cada capítulo cita la definición de cátedra antes de ampliar. Los agregados de UTN/UP/UNLP están identificados como "complemento" y no se cuentan como cobertura oficial.

## D.4 Huecos declarados y cómo se cubren

| Hueco | Estado |
|---|---|
| M1L2 (aplicación en base de datos) no tenía capítulo | ✅ Cerrado: capítulo 2 |
| M3L4 (convenciones y tipos) no tenía capítulo | ✅ Cerrado: capítulo 14 |
| SELECT/JOIN/agrupamiento sin lectura propia | ✅ Cubiertos como complementos 15–18 |
| DCL sin lectura propia | ✅ Cubierto en 19 |
| PL/SQL sin lectura oficial (la cátedra usa MySQL) | ✅ 20–23 con equivalencias MySQL y Oracle |

## D.5 Qué quedó fuera (y por qué)

| Tema | Motivo |
|---|---|
| Transacciones y ACID | Fuera del programa S21; anexo E por si se toma |
| Optimización con planes de ejecución (`EXPLAIN`) | Se menciona como diagnóstico, no se desarrolla |
| Réplica, particionado, clustering | Fuera del alcance del EFIP |
| NoSQL | Fuera del programa |
| Administración avanzada (backup, tuning) | Solo lo mínimo del rol DBA en el capítulo 2 |

## D.6 Enlaces con los otros libros

| Tema | Se profundiza en |
|---|---|
| Modelo entidad-relación como insumo del diseño de software | [[ad10_modelo-analisis\|Libro 3 — Análisis y Diseño]] |
| Tipos y estructuras en Java | [[00_Inicio\|Libro 1 — Programación]] |
| Redes y acceso a la base | [[00_Inicio_CM\|Libro 4 — Comunicaciones]] |

#libro2 #mapa
