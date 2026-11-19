---
tags: [efip, analisis-diseno, anexo, errores]
libro: 3
anexo: C
---

# C. Errores frecuentes — Análisis y Diseño

> [!info] Cómo usarlo
> Antes del simulacro, leé solo esta lista. Después, marcá los que cometiste.

## C.1 Conceptos

| Error | Corrección |
|---|---|
| “UML es una metodología” | Es un lenguaje; el PUD es el proceso |
| Confundir proceso, modelo y metodología | Definir los tres |
| Confundir fase con iteración | La fase contiene iteraciones |
| Decir que el PUD es cascada | Es iterativo e incremental |
| Mezclar análisis y diseño | Qué vs. cómo |
| “El modelo es la realidad” | Es una simplificación |

## C.2 Requerimientos

| Error | Corrección |
|---|---|
| RNF sin métrica | Agregar número y verificación |
| RF con dos verbos | Un requisito por función |
| RF que describe la interfaz | Describir la función |
| Confundir restricción con RNF | Límite vs. calidad medible |
| Requisito no verificable | Reescribir con criterio de prueba |
| Historia sin “para” | No aporta valor |
| Omitir al actor | Indicar quién lo origina |

## C.3 Casos de uso

| Error | Corrección |
|---|---|
| Sistema como actor | Solo actores externos |
| CU sin actor | Todo CU tiene al menos uno |
| Invertir flechas de include/extend | Base → incluido; extendido → base |
| `extend` para lo obligatorio | `include` |
| Nombres con sustantivo | Verbo en infinitivo |
| Un CU que hace todo | Dividir por objetivo |
| Include/extend anidados sin necesidad | Simplificar |
| Especificar el CU incluido dentro del base | Referenciarlo |
| Errores en el escenario principal | Van en alternativos |
| Postcondición como lista de tablas | Usar estados del dominio |
| Precondición como acción | Debe ser un hecho |

## C.4 Modelo de dominio

| Error | Corrección |
|---|---|
| Empresa cliente como clase | No modelarla |
| `precio` suelto cuando se pide histórico | `ListaDePrecios` |
| `tipo` como texto | Clase `TipoX` |
| Atributos complejos dentro de la clase | Clase aparte |
| M:N sin clase asociativa | Crear la clase |
| Clases técnicas (`DAO`, `Service`) | Eso es diseño |
| Asociaciones sin multiplicidad | Agregarla |

## C.5 Análisis y diseño

| Error | Corrección |
|---|---|
| `DAO`/`Service` en análisis | Es diseño |
| Una clase “Sistema” que hace todo | Separar boundary/control/entity |
| Boundary accede directo a entity | Pasa por control |
| Entity conoce la pantalla | Dependencia invertida |
| Un control por método | Uno por CU |
| DCD sin tipos | Agregar tipos |
| Contrato imperativo | Postcondiciones declarativas |
| Asignar todo al controlador | Aplicar Experto y Creador |
| `if` por tipo | Polimorfismo |
| Cadenas `getA().getB()` | Ley de Demeter |

## C.6 Diagrama de secuencia

| Error | Corrección |
|---|---|
| Empezar a dibujar sin el CU | Numerá los pasos del escenario principal |
| Pantalla → Entidad | Pantalla → Control → Entidad/Repositorio |
| Actor a la derecha | El actor va primero, a la izquierda |
| Omitir retornos que se usan | Si el paso siguiente usa el dato, dibujalo |
| Crear el objeto arriba | La caja nueva aparece abajo, al crearse |
| `alt` para un if sin else | Va `opt` |
| Anidar marcos de más | Dos diagramas antes que uno ilegible |
| Mensajes que no están en el DCD | Filtro del paso 5: método y parámetros |
| Nombres vagos | Verbos del dominio (`registrar`, `buscar`) |
| Dibujar todos los escenarios juntos | Uno principal + alternativos complejos |

## C.7 Arquitectura

| Error | Corrección |
|---|---|
| Elegir estilo por moda | Justificar con atributos de calidad |
| Confundir arquitectura con despliegue | El despliegue es una vista |
| Lógica de negocio en la UI | Va en el dominio |
| Un subsistema por clase | Agrupar por responsabilidad |
| No documentar decisiones | Registrar ADR |
| Microservicios para todo | Evitar complejidad innecesaria |
| Pruebas solo funcionales | Incluir atributos de calidad |
| Integrar todo al final | Integración incremental |

## C.8 Checklist de 60 segundos (escrito)

- [ ] ¿Escribí 3 RF verificables y 3 RNF medibles?
- [ ] ¿Cada RF tiene actor y criterio?
- [ ] ¿El diagrama de CU tiene actores externos?
- [ ] ¿Cada CU tiene actor?
- [ ] ¿Las flechas de include/extend van en el sentido correcto?
- [ ] ¿El `extend` tiene punto de extensión?
- [ ] ¿Nombré los CU con verbo en infinitivo?
- [ ] ¿Justifiqué las relaciones?
- [ ] ¿El escenario principal no tiene errores?
- [ ] ¿La postcondición es un estado?

## C.9 Checklist de 60 segundos (oral)

- [ ] Puedo explicar por qué elegí cada include/extend.
- [ ] Puedo justificar cada clase del dominio.
- [ ] Sé diferenciar análisis de diseño.
- [ ] Sé nombrar el patrón GRASP usado y por qué.
- [ ] Puedo explicar una decisión arquitectónica con dos atributos de calidad.

#libro3 #anexo #errores
