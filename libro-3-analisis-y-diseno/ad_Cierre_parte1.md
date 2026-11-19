---
tags: [efip, analisis-diseno, cierre]
libro: 3
parte: 1
---

# Cierre de la Parte 1 — Fundamentos y UML

> [!info] Qué hacer con este archivo
> Verificación, no contenido nuevo.

## Checklist de la Parte 1

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Definir ingeniería de software, proceso y metodología | [[ad01_ingenieria-y-metodologia|Cap. 1]] | ☐ |
| Explicar por qué se modela y qué es un modelo | [[ad01_ingenieria-y-metodologia|Cap. 1]] | ☐ |
| Diferenciar modelo estructural de comportamiento | [[ad01_ingenieria-y-metodologia|Cap. 1]] | ☐ |
| Comparar cascada, incremental y PUD | [[ad02_modelos-de-proceso-y-pud|Cap. 2]] | ☐ |
| Nombrar las tres características del PUD | [[ad02_modelos-de-proceso-y-pud|Cap. 2]] | ☐ |
| Ubicar cada fase, su objetivo y su hito | [[ad02_modelos-de-proceso-y-pud|Cap. 2]] | ☐ |
| Distinguir fase, iteración e incremento | [[ad02_modelos-de-proceso-y-pud|Cap. 2]] | ☐ |
| Explicar por qué UML no es metodología | [[ad03_uml-lenguaje|Cap. 3]] | ☐ |
| Nombrar bloques y relaciones | [[ad03_uml-lenguaje|Cap. 3]] | ☐ |
| Aplicar visibilidad y estereotipos | [[ad03_uml-lenguaje|Cap. 3]] | ☐ |
| Elegir el diagrama correcto | [[ad04_diagramas-y-vistas|Cap. 4]] | ☐ |
| Explicar las cinco vistas del 4+1 | [[ad04_diagramas-y-vistas|Cap. 4]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| Proceso | Metodología | Actividades vs. filosofía + fases + técnicas + reglas + herramientas |
| Cascada | PUD | Secuencial vs. iterativo e incremental |
| Fase | Iteración | Etapa con hito vs. miniproyecto que produce un incremento |
| UML | PUD | Lenguaje vs. proceso |
| Estructural | Comportamiento | Organización vs. dinámica |
| Componente | Nodo | Software vs. hardware |
| Vista lógica | Vista de despliegue | Clases vs. servidores |

## Ejercicio integrador de la Parte 1

> [!example] Enunciado (15 minutos)
> 1. Ubicá estas actividades en la fase del PUD: definir alcance, estabilizar la arquitectura, implementar funcionalidad restante, corregir errores reportados por el cliente.
> 2. Elegí el diagrama para: (a) estados de una alerta, (b) colaboración de objetos, (c) máquinas donde corre el sistema, (d) actores y funcionalidad.
> 3. Explicá en 3 líneas por qué UML no es una metodología.

> [!success]- Solución
> **1.** Inicio: definir alcance. Elaboración: estabilizar arquitectura. Construcción: implementar el resto. Transición: corregir lo reportado.
> **2.** (a) estados; (b) secuencia o comunicación; (c) despliegue; (d) casos de uso.
> **3.** Porque UML solo aporta notación y reglas de buena formación; no define qué artefactos hacer, en qué orden ni con qué criterios. Eso lo aporta el proceso (PUD).

## Oral de la Parte 1 (8 preguntas)

> [!question]- 1. ¿Qué es una metodología?
> Conjunto de filosofías, fases, procedimientos, reglas, técnicas, herramientas, documentación y formación para desarrollar sistemas.

> [!question]- 2. ¿Por qué se modela?
> Para comprender, visualizar, especificar, documentar y construir, reduciendo la complejidad y detectando errores temprano.

> [!question]- 3. ¿Qué caracteriza al PUD?
> Dirigido por casos de uso, centrado en la arquitectura, iterativo e incremental.

> [!question]- 4. ¿Cuáles son las fases y sus hitos?
> Inicio (objetivo del ciclo), Elaboración (arquitectura), Construcción (capacidad operativa inicial), Transición (release).

> [!question]- 5. ¿Qué diferencia hay entre fase e iteración?
> La fase es una etapa con un hito; la iteración es un miniproyecto dentro de la fase que produce un incremento.

> [!question]- 6. ¿UML es una metodología?
> No: es un lenguaje de modelado independiente del proceso.

> [!question]- 7. ¿Qué es el modelo 4+1?
> Cuatro vistas (lógica, procesos, implementación, despliegue) más los escenarios (casos de uso) que las validan.

> [!question]- 8. ¿Qué diferencia hay entre análisis y diseño?
> El análisis responde qué debe hacer el sistema; el diseño, cómo se implementa.

## Lo que sigue

[[ad05_modelo-de-negocio|Modelo de negocio y modelo de dominio]].

#libro3 #cierre #fundamentos
