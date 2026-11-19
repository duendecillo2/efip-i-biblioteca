---
tags: [efip, analisis-diseno, anexo, plantillas]
libro: 3
anexo: A
---

# A. Plantillas para el escrito

> [!info] Para qué sirve
> Lo que se copia a mano en el examen y en los simulacros. Practicá completarlas en 35 minutos.

## A.1 Requerimientos

### Funcional

```text
RF-<n>: El sistema debe <verbo> <objeto> [<condición>].
Actor: <quién lo origina>
Criterio de aceptación: <cómo se verifica>
```

### No funcional

```text
RNF-<n>: <categoría>.
El sistema debe <métrica> bajo <condición>.
Verificación: <método>.
```

### Historia de usuario

```text
Como <rol> necesito <funcionalidad> para <beneficio>.

Conversación: <preguntas pendientes>
Criterios de aceptación:
- Si <condición> entonces <acción>.
```

## A.2 Caso de uso: especificación

```text
ID:
Paquete:
Prioridad (1-5):
Categoría (esencial/soporte):
Complejidad (baja/media/alta):
Actores (principal/secundario):
Stakeholders:
Tipo (concreto/abstracto):
Objetivo:

Precondiciones:
- ...

Postcondiciones:
- ...

Escenario principal:
1. ...
2. ...

Alternativos:
A1. En el paso N, si <condición>: <acción>.
A2. ...

Reglas de negocio:
- ...

RNF asociados:
- ...

Incluye: CU-xx <nombre>
Extiende: CU-yy <nombre> (punto de extensión: <...>)
```

## A.3 Contrato de operación

```text
Operación: <nombre>(<parámetros>)
Referencias: CU-xx / RF-xx

Precondiciones:
- ...

Postcondiciones:
- Se creó/eliminó una instancia de <Clase>.
- Se modificó <atributo> a <valor>.
- Se creó/rompió la asociación <A>–<B>.
- <Objeto> quedó en estado <ESTADO>.
```

## A.4 Modelo de dominio: checklist

- [ ] ¿Está lo que se vende o gestiona?
- [ ] ¿Los tipos y estados son clases simples?
- [ ] ¿Los atributos complejos son clases?
- [ ] ¿La empresa cliente **no** está?
- [ ] ¿Las M:N con atributos tienen clase asociativa?
- [ ] ¿Hay clase de precios si se pide histórico?
- [ ] ¿Todas las asociaciones tienen multiplicidad?

## A.5 DCD: checklist

- [ ] Tipos en atributos y retornos
- [ ] Visibilidad (`-`, `+`, `#`)
- [ ] Navegabilidad en las asociaciones
- [ ] Multiplicidades
- [ ] Enumeraciones para estados
- [ ] Métodos con firma
- [ ] Sin clases de análisis (`<<boundary>>`), salvo que se pida

## A.6 Caso de prueba

```text
ID: CP-xx
Nivel: unidad / integración / sistema / aceptación
Cubre: CU-xx / RF-xx
Precondición:
Entrada:
Pasos:
Resultado esperado:
Resultado obtenido:
Estado: aprobado / fallido
```

## A.7 Arquitectura: descripción

```text
1. Contexto y alcance
2. Stakeholders y vistas elegidas
3. Vista lógica (subsistemas, clases clave)
4. Vista de implementación (componentes, interfaces)
5. Vista de despliegue (nodos, conexiones)
6. Decisiones (ADR)
7. Atributos de calidad priorizados
8. Riesgos y pendientes
```

### ADR

```text
ADR-<n>: <título>
Contexto: <problema>
Decisión: <qué se eligió>
Alternativas: <qué se descartó y por qué>
Consecuencias: <ventajas y costos>
Estado: propuesta / aceptada / reemplazada
```

## A.8 Diagrama de casos de uso: checklist

- [ ] Actores externos (nunca el sistema)
- [ ] Todo CU tiene actor
- [ ] Nombres con verbo en infinitivo
- [ ] `include` desde base a incluido
- [ ] `extend` desde extendido a base
- [ ] Punto de extensión indicado
- [ ] Sin include/extend anidados innecesarios
- [ ] Un ABM por entidad usada

## A.9 Guion de 35 minutos

| Min | Actividad | Entregable |
|---|---|---|
| 0–8 | Leer, subrayar, identificar actores | Notas |
| 8–20 | 3 RF + 3 RNF | Tabla |
| 20–30 | Diagrama de CU | Diagrama |
| 30–35 | Relaciones y justificación | Texto |

> [!tip] Si el caso es largo
> Priorizá: **RF/RNF + CU + relaciones**. El diagrama de clases y el DER son para el oral o para mesas con más tiempo.

#libro3 #anexo #plantillas

## A.10 Diagrama de secuencia: plantilla y checklist

**Receta de 5 pasos**

| Paso | Qué hacés | Producto |
|---|---|---|
| 1 | Tomás el escenario principal del CU | Lista de mensajes actor → sistema |
| 2 | Ordenás las líneas de vida | Actor → Boundary → Control → Entidad/Repositorio |
| 3 | Elegís el tipo de flecha | Síncrona, retorno, creación |
| 4 | Agregás marcos solo si hay condición o bucle | `alt`, `opt`, `loop` |
| 5 | Verificás contra el DCD | Métodos, parámetros y visibilidad |

**Plantilla para papel**

```text
Actor → «boundary» PantallaX → «control» ControlX → «entity» Entidad
                                              ↘ «repository» RepositorioX
                                              ↘ «service» ServicioY

1. Actor → Pantalla: operación(args)
2. Pantalla → Control: operación(args)
3. Control → Repositorio: buscar(args)
4. Repositorio → Control: objeto        (retorno, si se usa)
5. Control → Entidad: operación(args)
   [alt condición]
6.     Control → Servicio: notificar(...)
   [else]
7.     Control → Control: caso normal
   [end]
8. Control → Pantalla: resultado
9. Pantalla → Actor: mensaje
```

**Checklist de entrega**

| ✔ | Verificación |
|---|---|
| ☐ | Cada paso del escenario principal tiene su mensaje |
| ☐ | El actor está a la izquierda y la pantalla no habla con la entidad |
| ☐ | Los retornos que se usan están dibujados |
| ☐ | El objeto creado aparece abajo, con flecha de creación |
| ☐ | `alt` solo con else; `opt` para if simple; `loop` para colecciones |
| ☐ | Cada mensaje existe en el DCD con los mismos parámetros |
| ☐ | La emisora tiene visibilidad hacia la receptora |
| ☐ | Los nombres son verbos del dominio |
