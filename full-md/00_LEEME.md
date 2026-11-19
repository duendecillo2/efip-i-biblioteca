# Libros en Markdown de un solo archivo

Tres niveles de concatenación, listos para abrir en Obsidian y exportar a PDF.

## Nivel 1 — Por sección

Carpeta `secciones/`. Un archivo por parte o módulo, con portada, índice interno y capítulos.

| Archivo | Sección | Notas |
|---|---|---|
| `L1_S1_Parte_1_Fundamentos.md` | Libro 1 · Fundamentos y Java | 3 |
| `L1_S2_Parte_2_POO.md` | Libro 1 · POO | 8 |
| `L1_S3_Parte_3_Complementarios.md` | Libro 1 · Complementarios | 4 |
| `L1_S4_Parte_4_Estructuras.md` | Libro 1 · Estructuras y ordenación | 5 |
| `L1_S5_Anexos.md` | Libro 1 · Anexos | 4 |
| `L2_S1_M1_Motores.md` | Libro 2 · Módulo 1 | 6 |
| `L2_S2_M2_Diseno.md` | Libro 2 · Módulo 2 | 6 |
| `L2_S3_M3_SQL.md` | Libro 2 · Módulo 3 | 10 |
| `L2_S4_M4_Procedimental.md` | Libro 2 · Módulo 4 | 7 |
| `L2_S5_Anexos.md` | Libro 2 · Anexos | 5 |
| `L3_S1_1_1_Analisis_y_Diseno.md` | Libro 3 · Sub-eje 1.1 | 5 |
| `L3_S2_1_2_PUD.md` | Libro 3 · Sub-eje 1.2 | 12 |
| `L3_S3_2_1_Arquitectura.md` | Libro 3 · Sub-eje 2.1 | 3 |
| `L3_S4_Anexos.md` | Libro 3 · Anexos | 5 |
| `L4_S1_6_1_Fundamentos.md` | Libro 4 · Sub-eje 6.1 | 5 |
| `L4_S2_6_2_Fisica.md` | Libro 4 · Sub-eje 6.2 | 5 |
| `L4_S3_6_3_Enlace.md` | Libro 4 · Sub-eje 6.3 | 4 |
| `L4_S4_6_4_Redes.md` | Libro 4 · Sub-eje 6.4 | 6 |
| `L4_S5_Anexos.md` | Libro 4 · Anexos | 4 |

## Nivel 2 — Por libro

| Archivo | Contenido | Palabras |
|---|---|---|
| `Libro_1_Programacion.md` | 20 capítulos + 4 anexos | ~40.700 |
| `Libro_2_Base_de_Datos.md` | 25 capítulos + 4 cierres + 5 anexos | ~46.700 |
| `Libro_3_Analisis_y_Diseno.md` | 17 capítulos + 3 cierres + 5 anexos | ~30.300 |
| `Libro_4_Comunicaciones.md` | 16 capítulos + 4 cierres + 4 anexos | ~29.200 |

## Nivel 3 — Todo

| Archivo | Contenido | Palabras |
|---|---|---|
| `Biblioteca_EFIP_I_Completa.md` | Los cuatro libros, con portada e índice de cada uno | ~147.100 |

## Cómo exportar desde Obsidian

1. Copiá el `.md` que quieras a tu bóveda (o abrí esta carpeta como bóveda).
2. Abrilo en **modo lectura** y verificá que los diagramas Mermaid se dibujen.
3. `Ctrl/Cmd + P` → **Export to PDF**.
4. Elegí **A4** y márgenes normales.

> [!tip] Si los saltos de página no se respetan
> Cada capítulo va precedido por `<div style="page-break-after: always;"></div>`. Si tu versión de Obsidian los ignora, usá el plugin **Better Export PDF** o exportá con Chrome desde el HTML.

## Qué se conservó

- **Callouts** de Obsidian, con color.
- **Diagramas Mermaid** (186 en todo el vault; 44 en el Libro 1).
- **Tablas, código Java/SQL y fórmulas** `$$...$$`.
- **Portada, índice y presentación** en los niveles 2 y 3.

## Qué se transformó

| En las notas | En el archivo único |
|---|---|
| `[[cm13_direccionamiento-ip\|capítulo 13]]` | `capítulo 13` (texto) |
| Frontmatter de cada nota | Se quitó; queda uno por archivo |
| Etiquetas `#libro4 #redes` | Se quitaron |
| "Lo que sigue" al final de cada capítulo | Se quitó |
| Callouts plegables `[!example]-` | Se abrieron, para que la solución se vea en el PDF |
| Un archivo por capítulo | Un `#` por capítulo, con salto de página |

> [!note] Relación con `libros_pdf/`
> Los PDF de `libros_pdf/` son la versión maquetada (portada, índice con números de página, tipografía de imprenta). Estos Markdown son la versión editable y exportable.
