---
tags: [efip, analisis-diseno, anexo, oral]
libro: 3
anexo: B
---

# B. Banco de preguntas de oral — Análisis y Diseño

> [!info] Cómo usarlo
> Tapá la respuesta, contestá en voz alta y recién después abrí. Aplicá la regla del EFIP: definir → cómo funciona → aplicar al caso → justificar.

## 1.1 — Ingeniería de software y PUD

> [!question]- 1. ¿Qué es la ingeniería de software?
> Disciplina que aplica un enfoque sistemático, disciplinado y cuantificable a todos los aspectos del desarrollo, desde la especificación hasta el mantenimiento.

> [!question]- 2. Proceso, modelo de proceso y metodología.
> Proceso: actividades. Modelo: orden de esas actividades. Metodología: filosofía + fases + procedimientos + reglas + técnicas + herramientas + documentación + formación.

> [!question]- 3. ¿Por qué se modela?
> Para comprender, visualizar, especificar, documentar y construir, reduciendo complejidad y detectando errores temprano.

> [!question]- 4. Modelo estructural y de comportamiento.
> El estructural resalta la organización; el de comportamiento, la dinámica.

> [!question]- 5. ¿Qué caracteriza al PUD?
> Dirigido por casos de uso, centrado en la arquitectura, iterativo e incremental.

> [!question]- 6. Fases y hitos del PUD.
> Inicio (objetivo del ciclo), Elaboración (arquitectura), Construcción (capacidad operativa inicial), Transición (release).

> [!question]- 7. Fase, iteración e incremento.
> La fase es una etapa con hito; la iteración es un miniproyecto dentro de la fase; el incremento es el crecimiento del producto.

> [!question]- 8. ¿En qué fase se estabiliza la arquitectura?
> En Elaboración, cuyo hito es *Lifecycle Architecture*.

> [!question]- 9. ¿UML es una metodología?
> No: es un lenguaje de modelado independiente del proceso.

> [!question]- 10. ¿Qué es el 4+1?
> Cuatro vistas (lógica, procesos, implementación, despliegue) más los escenarios (CU) que las validan.

## 1.2 — Negocio, requisitos y casos de uso

> [!question]- 11. Actor de negocio vs. actor del sistema.
> El de negocio está fuera del negocio; el del sistema interactúa con el software.

> [!question]- 12. ¿Qué es un caso de uso de negocio?
> Una secuencia que produce un resultado observable de valor para un actor del negocio.

> [!question]- 13. ¿Qué es un trabajador de negocio?
> Un rol interno que ejecuta el proceso y manipula entidades de negocio.

> [!question]- 14. ¿Qué es una entidad de negocio?
> Algo que los trabajadores toman, inspeccionan, producen o usan al ejecutar el CU de negocio.

> [!question]- 15. ¿Qué es el modelo de dominio?
> Un modelo conceptual de las clases del problema, con atributos y asociaciones, sin decisiones de implementación.

> [!question]- 16. ¿La empresa cliente va como clase?
> No. El modelo de dominio no incluye a la empresa para la que se desarrolla.

> [!question]- 17. ¿Cuándo un atributo es clase?
> Cuando tiene atributos propios o representa un tipo/estado con valores predefinidos.

> [!question]- 18. ¿Cómo se modelan los tipos y estados?
> Como clases simples con un atributo descriptivo (o enumeraciones si son finitos).

> [!question]- 19. ¿Qué es un requerimiento funcional?
> Una función que el sistema debe realizar, transformando entradas en salidas.

> [!question]- 20. ¿Qué es un requerimiento no funcional?
> Una restricción de calidad medible: rendimiento, seguridad, usabilidad, disponibilidad.

> [!question]- 21. ¿Cómo se escribe un RNF?
> Con categoría, métrica, condición y método de verificación.

> [!question]- 22. ¿Qué es una restricción?
> Un límite impuesto a la solución (tecnología, norma, plazo), distinto de un RNF.

> [!question]- 23. ¿Qué es un actor?
> Todo lo externo al sistema que interactúa con él; nunca el sistema mismo.

> [!question]- 24. Actor primario y secundario.
> El primario inicia el CU y obtiene el valor; el secundario se ve afectado o participa sin iniciar.

> [!question]- 25. `include` vs. `extend`.
> `include` es obligatorio y siempre ocurre (base → incluido); `extend` es opcional bajo condición (extendido → base).

> [!question]- 26. ¿Qué es un punto de extensión?
> La condición (verdadero/falso) que habilita el `extend`.

> [!question]- 27. ¿Cuándo generalización de CU?
> Cuando hay variantes del mismo objetivo que comparten comportamiento.

> [!question]- 28. ¿Un RF es un CU?
> Generalmente sí: son dos formas de modelar requerimientos funcionales.

> [!question]- 29. ¿Qué es la especificación de un CU?
> La descripción completa de su comportamiento: actores, precondiciones, escenarios, postcondiciones, reglas y RNF.

> [!question]- 30. ¿Qué va en el escenario principal?
> El camino sin errores; los errores van en los alternativos.

> [!question]- 31. Precondición vs. postcondición.
> La precondición es un hecho que debe cumplirse antes; la postcondición, un estado que queda después.

> [!question]- 32. ¿Puede una postcondición ser un estado?
> Sí: “la póliza queda vigente”.

> [!question]- 33. ¿Cómo se referencia un include?
> “El sistema ejecuta CU-xx”, sin copiar sus pasos.

> [!question]- 34. ¿Qué es una historia de usuario?
> Una especificación ligera con tarjeta, conversación y criterios de aceptación.

> [!question]- 35. ¿Qué pasa si no puedo definir el “para” de una historia?
> La funcionalidad no aporta valor: hay que reescribirla o descartarla.

## 1.2 — Prototipos, análisis y diseño

> [!question]- 36. ¿Para qué sirve un prototipo?
> Para validar requisitos, detectar ambigüedades y obtener preferencias, con participación del usuario.

> [!question]- 37. Tipos de prototipo.
> Parcheado (operacional), no operacional (maqueta) y primero de una serie (piloto).

> [!question]- 38. ¿Qué riesgo tiene el prototipo parcheado?
> Que se lo entregue como producto: su código no tiene calidad.

> [!question]- 39. ¿Qué es una clase de análisis?
> Una abstracción clasificada como boundary, entity o control.

> [!question]- 40. Boundary, entity y control.
> Interfaz con el actor, información del dominio y coordinación del CU.

> [!question]- 41. ¿Puede una entidad conocer un boundary?
> No: la dependencia va del boundary al control y del control a la entidad.

> [!question]- 42. ¿Cuántos controles por CU?
> Uno por CU o por grupo cohesivo.

> [!question]- 43. ¿Qué agrega el modelo de diseño?
> Decisiones de implementación: tipos, visibilidad, navegabilidad, componentes, tecnología.

> [!question]- 44. ¿Qué es un contrato de operación?
> La descripción declarativa de pre y postcondiciones de una operación del sistema.

> [!question]- 45. Categorías de postcondición.
> Creación/eliminación de instancias, modificación de atributos, creación/ruptura de asociaciones.

> [!question]- 46. ¿Qué es el DCD?
> El diagrama de clases de diseño: clases de software con tipos, visibilidad, métodos y navegabilidad.

> [!question]- 47. SSD vs. secuencia de diseño.
> El SSD muestra al sistema como caja negra; la secuencia de diseño abre la caja y muestra objetos.

## 1.2 — Diagrama de secuencia

> [!question]- 48. ¿Para qué sirve un diagrama de secuencia?
> Para mostrar qué objetos colaboran en un CU y en qué orden se envían los mensajes. El tiempo va hacia abajo.

> [!question]- 49. ¿Cómo se ordenan las líneas de vida?
> Actor → Pantalla (boundary) → Controlador (control) → Entidad/Repositorio. La pantalla nunca habla directo con la entidad.

> [!question]- 50. Tres tipos de flecha.
> Síncrona (llamada), retorno (punteada) y creación (`new`, la caja aparece más abajo).

> [!question]- 51. ¿Cuándo se usa `alt`, `opt` y `loop`?
> `alt` para if/else, `opt` para if simple, `loop` para recorrer una colección.

> [!question]- 52. ¿Qué se verifica contra el DCD?
> Que el método exista con los mismos parámetros y que la clase emisora tenga visibilidad hacia la receptora.

## GRASP

> [!question]- 53. ¿Qué es GRASP?
> Patrones para asignar responsabilidades, buscando bajo acoplamiento y alta cohesión.

> [!question]- 54. Experto.
> Asignar la responsabilidad a quien tiene la información necesaria.

> [!question]- 55. Creador.
> Asignar la creación a quien contiene, registra, inicializa o usa exclusivamente al objeto.

> [!question]- 56. Controlador.
> Asignar los eventos del sistema a un objeto que representa el sistema, un subsistema o un CU.

> [!question]- 57. Bajo acoplamiento y alta cohesión.
> Minimizar dependencias y mantener responsabilidades relacionadas y pocas por clase.

> [!question]- 58. Polimorfismo (GRASP).
> Cuando el comportamiento varía por tipo, asignar la responsabilidad a los tipos que varían.

> [!question]- 59. Fabricación pura.
> Crear una clase de conveniencia que no es del dominio para lograr cohesión y desacople.

> [!question]- 60. Indirección.
> Poner un intermediario para que dos elementos no se acoplen directamente.

> [!question]- 61. Variaciones protegidas.
> Encapsular los puntos de cambio detrás de una interfaz estable.

> [!question]- 62. “No hables con extraños”.
> Solo enviar mensajes a self, parámetros, atributos, elementos de una colección propia u objetos creados en el método.

> [!question]- 63. GRASP vs. GoF.
> GRASP asigna responsabilidades; GoF es un catálogo de soluciones de diseño.

## 2.1 — Arquitectura

> [!question]- 64. ¿Qué es la arquitectura del software?
> La estructura del sistema, sus elementos y relaciones, y las decisiones significativas que habilitan atributos de calidad.

> [!question]- 65. Elementos clave.
> Subsistemas, componentes, interfaces, conectores y nodos.

> [!question]- 66. ¿Cómo se elige un estilo?
> Según los atributos de calidad priorizados y las restricciones del entorno.

> [!question]- 67. Capas y MVC.
> Capas separa presentación, aplicación, dominio y persistencia; MVC separa modelo, vista y controlador.

> [!question]- 68. ¿Qué es una decisión arquitectónica?
> Una elección estructural significativa y costosa de cambiar.

> [!question]- 69. ¿Qué documenta la descripción de la arquitectura?
> Vistas, subsistemas, interfaces, dependencias, componentes clave y decisiones.

> [!question]- 70. Integración incremental.
> Incorporar porciones pequeñas y ejecutables sobre una construcción anterior.

> [!question]- 71. Prueba de integración vs. de sistema.
> Entre componentes vs. sistema completo contra los requisitos.

> [!question]- 72. Verificación vs. validación.
> Cumplir la especificación vs. cumplir la expectativa del cliente.

> [!question]- 73. ¿Cómo se prueba un atributo de calidad?
> Con una prueba específica: carga para rendimiento, intento de acceso para seguridad, caída de nodo para disponibilidad.

#libro3 #anexo #oral
