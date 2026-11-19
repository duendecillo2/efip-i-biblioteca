---
tags: [efip, analisis-diseno, cierre]
libro: 3
parte: 2
---

# Cierre de la Parte 2 — Del negocio al diseño

> [!info] Qué hacer con este archivo
> Verificación de la parte más evaluada del módulo. Si algo falla, volvé al capítulo.

## Checklist de la Parte 2

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Distinguir actor, trabajador y entidad de negocio | [[ad05_modelo-de-negocio|Cap. 5]] | ☐ |
| Construir un modelo de dominio con las reglas de cátedra | [[ad05_modelo-de-negocio|Cap. 5]] | ☐ |
| Escribir 3 RF y 3 RNF verificables | [[ad06_requerimientos|Cap. 6]] | ☐ |
| Convertir un requerimiento en historia de usuario | [[ad06_requerimientos|Cap. 6]] | ☐ |
| Identificar actores y casos de uso | [[ad07_casos-de-uso|Cap. 7]] | ☐ |
| Decidir `include`, `extend` o generalización | [[ad07_casos-de-uso|Cap. 7]] | ☐ |
| Completar la plantilla de especificación de CU | [[ad08_especificacion-cu|Cap. 8]] | ☐ |
| Escribir escenario principal sin errores y alternativos | [[ad08_especificacion-cu|Cap. 8]] | ☐ |
| Elegir y justificar un prototipo | [[ad09_prototipos|Cap. 9]] | ☐ |
| Clasificar clases en boundary/entity/control | [[ad10_modelo-analisis|Cap. 10]] | ☐ |
| Escribir un contrato de operación | [[ad11_modelo-diseno|Cap. 11]] | ☐ |
| Dibujar un DCD con tipos y navegabilidad | [[ad11_modelo-diseno|Cap. 11]] | ☐ |
| Armar un diagrama de secuencia con la receta de 5 pasos | [[ad12_diagrama-de-secuencia|Cap. 12]] | ☐ |
| Ordenar líneas de vida y elegir el tipo de flecha | [[ad12_diagrama-de-secuencia|Cap. 12]] | ☐ |
| Usar `alt`, `opt` y `loop` con criterio | [[ad12_diagrama-de-secuencia|Cap. 12]] | ☐ |
| Verificar cada mensaje contra el DCD | [[ad12_diagrama-de-secuencia|Cap. 12]] | ☐ |
| Aplicar los nueve patrones GRASP | [[ad13_grasp|Cap. 13]] | ☐ |
| Armar componentes y despliegue | [[ad14_implementacion|Cap. 14]] | ☐ |
| Derivar casos de prueba de los escenarios | [[ad15_pruebas|Cap. 15]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| Actor de negocio | Actor del sistema | Fuera del negocio vs. interactúa con el software |
| RF | RNF | Qué hace vs. con qué calidad |
| Restricción | RNF | Límite vs. calidad medible |
| `include` | `extend` | Obligatorio vs. opcional bajo condición |
| Escenario principal | Alternativo | Sin errores vs. desvíos |
| Análisis | Diseño | Conceptual vs. físico |
| Boundary | Entity | Interfaz vs. dominio |
| Contrato | Secuencia | Estado final garantizado vs. colaboración |
| GRASP | GoF | Asignar responsabilidades vs. catálogo de soluciones |
| Verificación | Validación | Especificación vs. expectativa |

## Ejercicio integrador de la Parte 2

> [!example] Enunciado (40 minutos)
> El municipio quiere registrar dispositivos y alertas. El operador da de alta el dispositivo, registra alertas con prioridad 1..5 y consulta las pendientes. Si la prioridad es 1, se notifica al supervisor.
>
> 1. Escribí 3 RF y 3 RNF.
> 2. Modelá los CU con un `include` y un `extend`.
> 3. Especificá `Registrar alerta`.
> 4. Analizá el CU (boundary/control/entity).
> 5. Asigná responsabilidades con GRASP y dibujá el DCD.
> 6. Escribí dos casos de prueba.

> [!success]- Solución
> **1.**
> ```text
> RF-01: registrar dispositivos con código único, tipo y ubicación.
> RF-02: registrar alertas asociadas a un dispositivo, con prioridad 1..5.
> RF-03: consultar alertas pendientes ordenadas por prioridad.
>
> RNF-01 (rendimiento): 95 % de consultas ≤ 2 s con 50 usuarios.
> RNF-02 (seguridad): solo usuarios autenticados; auditoría de altas.
> RNF-03 (usabilidad): alta de alerta en ≤ 3 min por operador nuevo.
> ```
> **2.** Operador → `Gestionar dispositivos`, `Registrar alerta`, `Consultar alertas`; Supervisor → `Recibir notificación`. `Registrar alerta` **include** `Validar dispositivo`; `Notificar crítica` **extend** de `Registrar alerta`.
> **3.** Ver [[ad08_especificacion-cu|Cap. 8 (8.6)]].
> **4.** `PantallaAlerta` (boundary), `ControlAlertas` (control), `Alerta`, `Dispositivo` (entity).
> **5.** `ControlAlertas` recibe el evento (Controlador); `Dispositivo.crearAlerta()` (Creador); `Alerta.getPrioridad()` (Experto); `Notificador` (Indirección); `RepositorioAlertas` (Fabricación pura).
> **6.**
> ```text
> CP-01: prioridad 1 → alerta PENDIENTE + notificación.
> CP-02: prioridad 6 → error, no se crea la alerta.
> ```

## Oral de la Parte 2 (10 preguntas)

> [!question]- 1. ¿Qué es un requerimiento funcional?
> Una función que el sistema debe realizar, describiendo la transformación de entradas en salidas.

> [!question]- 2. ¿Cómo se escribe un RNF?
> Con categoría, métrica, condición y método de verificación.

> [!question]- 3. ¿Qué es un caso de uso?
> Una unidad funcional completa que da un resultado de valor a un actor.

> [!question]- 4. `include` vs. `extend`.
> `include` es obligatorio y siempre ocurre (base → incluido); `extend` es opcional bajo condición (extendido → base).

> [!question]- 5. ¿Cómo se especifica un CU?
> Con la plantilla: ID, prioridad, actores, precondiciones, escenarios, postcondiciones, reglas, RNF, include/extend.

> [!question]- 6. ¿Qué va en el escenario principal?
> El camino sin errores. Los errores van en los alternativos.

> [!question]- 7. ¿Qué diferencia hay entre precondición y postcondición?
> La precondición es un hecho que debe cumplirse antes; la postcondición, un estado que queda después.

> [!question]- 8. ¿Qué es una clase de análisis?
> Una abstracción clasificada como boundary (interfaz), entity (dominio) o control (coordinación).

> [!question]- 9. ¿Qué agrega el diseño al análisis?
> Decisiones de implementación: tipos, visibilidad, navegabilidad, componentes, tecnología.

> [!question]- 10. ¿Qué es GRASP y para qué sirve?
> Un conjunto de patrones para asignar responsabilidades, buscando bajo acoplamiento y alta cohesión.

## Lo que sigue

[[ad16_arquitectura|Arquitectura: elementos, estilos y decisiones]].

#libro3 #cierre #diseno
