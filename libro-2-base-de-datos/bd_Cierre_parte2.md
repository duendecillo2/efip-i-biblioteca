---
tags: [efip, base-de-datos, cierre]
libro: 2
parte: 2
---

# Cierre del Módulo 2 — Análisis y diseño

> [!info] Qué hacer con este archivo
> Verificación de modelado y normalización. Si algo falla, volvé al capítulo.

## Checklist del Módulo 2

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Pasar de un enunciado a entidades y atributos | [[bd06_analisis-y-diseno\|Cap. 6]] | ☐ |
| Decidir si algo es atributo, entidad o relación | [[bd06_analisis-y-diseno\|Cap. 6]] | ☐ |
| Determinar cardinalidad y participación | [[bd06_analisis-y-diseno\|Cap. 6]] | ☐ |
| Justificar un valor nulo | [[bd06_analisis-y-diseno\|Cap. 6]] | ☐ |
| Dibujar un DER con notación correcta | [[bd09_der\|Cap. 9]] | ☐ |
| Modelar una entidad débil con clave parcial | [[bd09_der\|Cap. 9]] | ☐ |
| Convertir un DER a tablas con PK y FK | [[bd10_der-a-tablas\|Cap. 10]] | ☐ |
| Decidir dónde va la FK según la participación | [[bd10_der-a-tablas\|Cap. 10]] | ☐ |
| Resolver multivaluados, débiles y ternarias | [[bd10_der-a-tablas\|Cap. 10]] | ☐ |
| Elegir la estrategia de especialización por cobertura | [[bd10_der-a-tablas\|Cap. 10]] | ☐ |
| Detectar dependencias parciales y transitivas | [[bd07_normalizacion-1fn-3fn\|Cap. 7]] | ☐ |
| Diagnosticar anomalías en casos reales | [[bd08_normalizacion-casos\|Cap. 8]] | ☐ |
| Decidir cuándo hace falta BCNF | [[bd08_normalizacion-casos\|Cap. 8]] | ☐ |
| Justificar una desnormalización | [[bd08_normalizacion-casos\|Cap. 8]] | ☐ |
| Normalizar hasta 3FN paso a paso | [[bd07_normalizacion-1fn-3fn\|Cap. 7]] | ☐ |
| Explicar las tres anomalías | [[bd07_normalizacion-1fn-3fn\|Cap. 7]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| Entidad | Atributo | Tiene identidad y datos propios vs. describe a otra |
| 1:N | M:N | FK en el lado N vs. tabla puente |
| Participación total | Parcial | Obligatoria vs. opcional |
| Entidad fuerte | Débil | Clave propia vs. clave compuesta con identificadora |
| 1FN | 2FN | Atomicidad vs. dependencia de la clave completa |
| 2FN | 3FN | Dependencia parcial vs. transitiva |
| Multivalorado | Derivado | Varios valores vs. calculable |
| Normalizar | Desnormalizar | Eliminar redundancia vs. aceptarla con justificación |

## Ejercicio integrador del Módulo 2

> [!example] Enunciado (30 minutos)
> Una clínica registra **turnos**. De cada turno se guarda fecha, hora, paciente y médico. Un paciente tiene DNI, nombre, teléfono y obra social. Un médico tiene matrícula, nombre y especialidad. Un paciente puede tener muchos turnos; un médico atiende muchos turnos. Se quiere saber cuántos turnos atendió cada médico por especialidad.
>
> 1. Modelá el DER.
> 2. Pasalo a tablas con PK y FK.
> 3. Verificá 1FN, 2FN y 3FN.
> 4. Escribí la consulta del punto 4.

> [!success]- Solución
> **1. DER**
> ```mermaid
> erDiagram
>     PACIENTE ||--o{ TURNO : solicita
>     MEDICO ||--o{ TURNO : atiende
>     OBRA_SOCIAL ||--o{ PACIENTE : cubre
>     PACIENTE { int id PK
>                string dni UK
>                string nombre
>                string telefono
>                int id_obra FK }
>     MEDICO { int id PK
>              string matricula UK
>              string nombre
>              string especialidad }
>     TURNO { int id PK
>             datetime fecha_hora
>             int id_paciente FK
>             int id_medico FK }
>     OBRA_SOCIAL { int id PK
>                   string nombre }
> ```
> **2. Tablas**
> ```sql
> CREATE TABLE obra_social (
>     id     INT AUTO_INCREMENT PRIMARY KEY,
>     nombre VARCHAR(60) NOT NULL UNIQUE
> );
>
> CREATE TABLE paciente (
>     id          INT AUTO_INCREMENT PRIMARY KEY,
>     dni         VARCHAR(10) NOT NULL UNIQUE,
>     nombre      VARCHAR(60) NOT NULL,
>     telefono    VARCHAR(20),
>     id_obra     INT NULL,
>     FOREIGN KEY (id_obra) REFERENCES obra_social(id)
> );
>
> CREATE TABLE medico (
>     id          INT AUTO_INCREMENT PRIMARY KEY,
>     matricula   VARCHAR(20) NOT NULL UNIQUE,
>     nombre      VARCHAR(60) NOT NULL,
>     especialidad VARCHAR(40) NOT NULL
> );
>
> CREATE TABLE turno (
>     id          INT AUTO_INCREMENT PRIMARY KEY,
>     fecha_hora  DATETIME NOT NULL,
>     id_paciente INT NOT NULL,
>     id_medico   INT NOT NULL,
>     FOREIGN KEY (id_paciente) REFERENCES paciente(id),
>     FOREIGN KEY (id_medico) REFERENCES medico(id)
> );
> ```
> **3. Formas normales**
>
> | Tabla | 1FN | 2FN | 3FN | Justificación |
> |---|---|---|---|---|
> | `paciente` | ✅ | ✅ | ✅ | PK simple; `id_obra` es FK, no dependencia transitiva de datos |
> | `medico` | ✅ | ✅ | ✅ | Atributos dependen solo de `id` |
> | `turno` | ✅ | ✅ | ✅ | PK simple; paciente y médico por FK |
>
> **4. Consulta**
> ```sql
> SELECT m.especialidad, m.nombre, COUNT(*) AS turnos
> FROM turno t
> JOIN medico m ON m.id = t.id_medico
> GROUP BY m.especialidad, m.nombre
> ORDER BY m.especialidad, turnos DESC;
> ```
>
> **Qué evalúa el tribunal:** que la relación N:M entre paciente y médico se resuelva con `turno` (entidad asociativa con atributos propios), que no haya datos del médico repetidos en `turno` y que la consulta agrupe por especialidad.

## Oral del Módulo 2 (8 preguntas)

> [!question]- 1. ¿Qué es una entidad débil?
> Una entidad sin clave propia, que se identifica por la clave de otra entidad más una clave parcial.

> [!question]- 2. ¿Cómo se implementa una relación M:N?
> Con una tabla puente cuya PK es la combinación de las dos FK, más los atributos propios de la relación.

> [!question]- 3. ¿Qué es una dependencia funcional?
> Una relación `A → B` donde un valor de A determina un único valor de B.

> [!question]- 4. ¿Qué exige la 1FN?
> Que todos los valores sean atómicos: sin grupos repetitivos ni listas en una celda.

> [!question]- 5. ¿Cuándo importa la 2FN?
> Solo cuando la clave primaria es compuesta: exige que todo atributo no clave dependa de la clave completa.

> [!question]- 6. ¿Qué es una dependencia transitiva?
> `A → B` y `B → C`, con B no clave. Viola 3FN.

> [!question]- 7. Nombrá las tres anomalías.
> Inserción, modificación y borrado.

> [!question]- 8. ¿Normalizarías siempre hasta 3FN?
> Sí como punto de partida. Si necesito rendimiento, desnormalizo con una razón medida y documento cómo mantengo la consistencia.

## Lo que sigue

[[bd11_lenguaje-sql|11. El lenguaje SQL]].

#libro2 #cierre #basededatos
