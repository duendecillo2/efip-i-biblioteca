---
tags: [efip, analisis-diseno, cierre]
libro: 3
parte: 3
---

# Cierre de la Parte 3 — Arquitectura

> [!info] Qué hacer con este archivo
> Verificación de 2.1. Si algo falla, volvé a los capítulos 16 y 17.

## Checklist de la Parte 3

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Definir arquitectura y sus elementos clave | [[ad16_arquitectura|Cap. 16]] | ☐ |
| Explicar subsistema, componente, interfaz y conector | [[ad16_arquitectura|Cap. 16]] | ☐ |
| Relacionar arquitectura con atributos de calidad | [[ad16_arquitectura|Cap. 16]] | ☐ |
| Elegir y justificar un estilo | [[ad16_arquitectura|Cap. 16]] | ☐ |
| Registrar una decisión arquitectónica | [[ad17_documentacion-y-testeo|Cap. 17]] | ☐ |
| Documentar con vistas por stakeholder | [[ad17_documentacion-y-testeo|Cap. 17]] | ☐ |
| Explicar integración incremental | [[ad17_documentacion-y-testeo|Cap. 17]] | ☐ |
| Planificar pruebas de arquitectura | [[ad17_documentacion-y-testeo|Cap. 17]] | ☐ |
| Diferenciar verificación de validación | [[ad17_documentacion-y-testeo|Cap. 17]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| Arquitectura | Diseño detallado | Estructura global y decisiones vs. clases y métodos |
| Componente | Nodo | Software vs. hardware |
| Subsistema | Clase | Unidad implementable con interfaz vs. unidad lógica |
| Vista lógica | Despliegue | Estructura de clases vs. máquinas |
| Estilo | Patrón | Organización global vs. solución puntual |
| Integración | Sistema | Entre componentes vs. sistema completo |
| Verificación | Validación | Especificación vs. expectativa |
| ADR | Comentario | Decisión con alternativas y consecuencias vs. nota suelta |

## Ejercicio integrador de la Parte 3

> [!example] Enunciado (25 minutos)
> Para el sistema del municipio:
> 1. Definí cuatro subsistemas con su responsabilidad e interfaz.
> 2. Elegí un estilo y justificalo con dos atributos de calidad.
> 3. Dibujá el despliegue.
> 4. Escribí un ADR de una decisión.
> 5. Definí dos pruebas de arquitectura.

> [!success]- Solución
> **1.**
>
> | Subsistema | Responsabilidad | Interfaz |
> |---|---|---|
> | Presentación | Pantallas de operador y técnico | `IUI` |
> | Aplicación | Casos de uso y transacciones | `IAlertas`, `IReparaciones` |
> | Dominio | Reglas de prioridad y estados | `IDominio` |
> | Persistencia | Acceso a datos | `IRepositorio` |
>
> **2.** Capas + MVC. Justificación: **mantenibilidad** (cambiar la UI sin tocar el dominio) y **seguridad** (un único punto de acceso controlado).
> **3.** PC operador y móvil técnico → servidor de aplicación → servidor MySQL, con HTTPS y JDBC.
> **4.** ADR-01: “API única como acceso”. Alternativas: acceso directo a la base. Consecuencia: más latencia, mejor control y testeabilidad.
> **5.** Integración: API + repositorio persisten y recuperan. Rendimiento: 50 usuarios, p95 ≤ 2 s.

## Oral de la Parte 3 (8 preguntas)

> [!question]- 1. ¿Qué es la arquitectura del software?
> La estructura del sistema: sus elementos, sus relaciones y las decisiones significativas que habilitan los atributos de calidad.

> [!question]- 2. ¿Cuáles son los elementos clave?
> Subsistemas, componentes, interfaces, conectores y nodos.

> [!question]- 3. ¿Cómo elegís un estilo?
> Según los atributos de calidad priorizados y las restricciones; no por moda.

> [!question]- 4. ¿Qué es una decisión arquitectónica?
> Una elección estructural significativa, costosa de cambiar, que habilita casos de uso y calidades.

> [!question]- 5. ¿Qué documenta la descripción de la arquitectura?
> Vistas, subsistemas, interfaces, dependencias, componentes clave y decisiones.

> [!question]- 6. ¿Qué es la integración incremental?
> Incorporar porciones pequeñas y ejecutables sobre una construcción anterior, reduciendo el riesgo.

> [!question]- 7. ¿Qué diferencia hay entre prueba de integración y de sistema?
> La primera prueba la interacción entre componentes; la segunda, el sistema completo contra los requisitos.

> [!question]- 8. Verificación vs. validación.
> Verificación: cumple la especificación. Validación: cumple la expectativa del cliente.

## Fin del libro

> [!success] Terminaste el Libro 3
> Cubriste el Módulo 1 del EFIP: **1.1**, **1.2** y **2.1**, con el método de UTN (CU, especificación, dominio, análisis, GRASP, arquitectura).
>
> Practicá ahora con:
> - `PRACTICA_ANALISIS_Y_DISENO/00_GUIA_PRACTICA.md`
> - `PRACTICA_ANALISIS_Y_DISENO/SIMULACROS/` (4 escritos completos)
> - [[ad_A_Plantillas|A. Plantillas]]
> - [[ad_B_Banco_preguntas|B. Banco de preguntas]]

#libro3 #cierre #arquitectura
