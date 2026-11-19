---
tags: [efip, analisis-diseno, anexo, mapa]
libro: 3
anexo: D
---

# D. Mapa del programa y trazabilidad — Análisis y Diseño

> [!info] Para qué sirve
> Ver qué sub-eje cubre cada capítulo y de qué documento sale.

## D.1 Cobertura del programa

| Sub-eje oficial | Capítulos | Estado |
|---|---|---|
| **1.1** Análisis y diseño de software: modelos y metodologías, etapas y fases del PUD, UML | [[ad01_ingenieria-y-metodologia\|1]] · [[ad02_modelos-de-proceso-y-pud\|2]] · [[ad03_uml-lenguaje\|3]] · [[ad04_diagramas-y-vistas\|4]] | ✅ Completo |
| **1.2** PUD: modelo de negocio, captura de requerimientos, modelo de casos de uso, prototipos, modelo del análisis, modelo de diseño, implementación, pruebas | [[ad05_modelo-de-negocio\|5]] · [[ad06_requerimientos\|6]] · [[ad07_casos-de-uso\|7]] · [[ad08_especificacion-cu\|8]] · [[ad09_prototipos\|9]] · [[ad10_modelo-analisis\|10]] · [[ad11_modelo-diseno\|11]] · [[ad12_diagrama-de-secuencia\|12]] · [[ad13_grasp\|13]] · [[ad14_implementacion\|14]] · [[ad15_pruebas\|15]] | ✅ Completo |
| **2.1** Arquitectura: elementos clave, diseño, documentación, implementación y testeo | [[ad16_arquitectura\|16]] · [[ad17_documentacion-y-testeo\|17]] | ✅ Completo |

## D.2 Fuente de cada bloque

| Bloque | Base Siglo 21 | Complemento |
|---|---|---|
| 1.1 | `EFIP_BASE_S21/1.1_UML_y_modelos/` — INF390 M1 L1–L4 + Ingeniería de Software M1 | UTN **Diseño de Sistemas** U1 (introducción), U3 (UML estático) |
| 1.2 | `EFIP_BASE_S21/1.2_PUD/` — M2 L1–L4 y M3 L1–L4 | UTN **Análisis de Sistemas** (`apuntes de clase practica asi.docx`, TP2, TP4) y **Diseño de Sistemas** (Larman: DSS y un diagrama por escenario principal, prototipos, OCL); **UP** Análisis de Sistemas clases 09–10 (diagramas de secuencia, interfaz/entidad/control) |
| 2.1 | `EFIP_BASE_S21/2.1_Arquitectura/` — M4 L1–L4 | UTN U8 (despliegue y evolución), U3 (componentes), U4 (GUI); UP/UNLP (vistas y documentación) |
| Anexo E | — | UTN U3 (OCL, GoF), **fuera del programa S21** |

> [!important] El método es de UTN
> - **Casos de uso y especificación:** reglas del apunte de práctica (`include`/`extend`, actores, escenarios, plantilla).
> - **Modelo de dominio:** heurísticas (tipos/estados como clase, no empresa, precio histórico, M:N asociativa).
> - **Diseño:** Larman (SSD, contratos, DCD) y **GRASP**.
> - **Arquitectura:** capas, MVC y 4+1.

## D.3 Huecos declarados

| Tema | Situación |
|---|---|
| UML con figuras | El texto de S21 pierde las figuras al extraerse; se compensa con UTN U3 |
| Taxonomía de “elementos clave” de arquitectura | S21 la menciona sin desarrollarla; se completó con UTN/UP |
| OCL y GoF | UTN los dicta; S21 no los pide. Van en el anexo E, opcional |
| Métricas de calidad | Fuera del alcance |

## D.4 Qué quedó fuera

| Tema | Motivo |
|---|---|
| Scrum, Kanban, SAFe | El programa pide modelos y metodologías en el marco del PUD/UML |
| BPMN y SysML | Notaciones de proceso/ingeniería de sistemas, fuera del eje |
| TOGAF, ITIL, COBIT | Gobierno y operación de TI |
| CMMI y métricas de proceso | Gestión de calidad, no análisis/diseño |
| Patrones GoF en profundidad | Catálogo adicional, no obligatorio |
| Arquitectura de microservicios en detalle | Se menciona como estilo |

## D.5 Autoevaluación final

| Nivel | Criterio | ✔ |
|---|---|---|
| 1 | Explico las 73 preguntas del [[ad_B_Banco_preguntas\|banco]] sin leer | ☐ |
| 2 | Completo la [[ad_A_Plantillas\|plantilla de CU]] en 10 minutos | ☐ |
| 3 | Escribo 3 RF + 3 RNF en 12 minutos | ☐ |
| 4 | Dibujo el diagrama de CU en 10 minutos y justifico cada relación | ☐ |
| 5 | Paso de CU a DCD aplicando GRASP | ☐ |
| 6 | Documento una arquitectura con vistas y un ADR | ☐ |

> [!success] Criterio de aprobación
> Si podés hacer 2, 3, 4 y 5, estás en condiciones de rendir el módulo. El 6 es para el oral.

## D.6 Cómo seguir

- Volver al [[00_Inicio_AD|índice del Libro 3]].
- Volver al [[00_Inicio|índice general]].
- Practicar en `PRACTICA_ANALISIS_Y_DISENO/` (4 simulacros completos).
- Continuar con el Libro 4 (Comunicaciones).

#libro3 #anexo #mapa
