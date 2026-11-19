---
tags: [efip, comunicaciones, fundamentos]
libro: 4
capitulo: 1
subeje: "6.1"
---

# 1. Sistemas de comunicación y normalización

> [!info] Al terminar este capítulo tenés que poder
> - Nombrar los elementos de un sistema de comunicación.
> - Explicar qué es un protocolo y una arquitectura de red.
> - Justificar la necesidad de normalización.
> - Distinguir transmisión de datos de otros tipos de comunicación.

> [!abstract] Qué debés saber (nivel 1)
> - **Sistema de comunicaciones:** fuente → transductor → transmisor → medio → receptor → transductor → destino.
> - **Transmisión de datos:** desplazamiento de información codificada en binario sobre un sistema de transmisión.
> - **Protocolo:** reglas acordadas para intercambiar información.
> - **Arquitectura de red:** conjunto de protocolos compatibles.
> - **Normalización:** directrices comunes para que equipos de distintos fabricantes se entiendan.
> - Organismos: ISO, IEEE, ITU-T, IETF.

## 1.1 Elementos de un sistema de comunicación

> [!quote] Definición de cátedra
> **Sistema de comunicaciones:** sistema compuesto por una fuente, un transductor de salida, un transmisor, un medio de transmisión, un receptor, un transductor de entrada y la colectora o destino de los datos.

```mermaid
flowchart LR
    F["Fuente"] --> TS["Transductor<br/>de salida"]
    TS --> TX["Transmisor"]
    TX --> M["Medio de<br/>transmisión"]
    M --> RX["Receptor"]
    RX --> TR["Transductor<br/>de entrada"]
    TR --> D["Destino"]
```

| Elemento | Función | Ejemplo |
|---|---|---|
| **Fuente** | Genera la información | Micrófono, sensor, teclado |
| **Transductor de salida** | Convierte a señal | Micrófono → tensión |
| **Transmisor** | Acondiciona la señal | Módem, tarjeta de red |
| **Medio** | Transporta | Cable, fibra, aire |
| **Receptor** | Recupera la señal | Módem, NIC |
| **Transductor de entrada** | Vuelve a información | Parlante, pantalla |
| **Destino** | Usa la información | Persona, sistema |

### DTE y DCE

| Sigla | Nombre | Función | Ejemplo |
|---|---|---|---|
| **DTE (ETD)** | Equipo Terminal de Datos | Genera o consume los datos: es fuente o destino | PC, router, terminal |
| **DCE (ETCD)** | Equipo de Terminación del Circuito de Datos | Adapta la señal del DTE al canal y suele aportar el reloj | Módem, códec, ONT |

> [!important] Quién es quién
> El **DTE** pone los datos; el **DCE** los adapta al medio y suele dar el reloj. En RS-232 la PC es DTE y el módem, DCE.

### Funciones generales del sistema

| Función | Para qué |
|---|---|
| Uso eficiente del medio | Multiplexación y compartición de la capacidad |
| Interfaces | Características mecánicas, eléctricas, funcionales y procedimentales |
| Generación y codificación | Producir señales que se propaguen y se interpreten |
| Sincronización | Inicio, fin y duración de cada elemento transmitido |
| Detección y control de errores | Verificar integridad y decidir si se retransmite |
| Control de flujo | Evitar que un emisor rápido desborde al receptor |
| Direccionamiento y encaminamiento | Identificar extremos y elegir el camino |

> [!important] La distinción que se pregunta
> **Transmisión de datos** es el desplazamiento de información **ya codificada en binario** sobre un sistema de transmisión eléctrica. No es “hablar por teléfono”: la voz analógica se digitaliza primero.

## 1.2 Protocolos y arquitectura

| Concepto | Definición | Ejemplo |
|---|---|---|
| **Protocolo** | Conjunto de reglas acordadas entre participantes | TCP, IP, HTTP |
| **Arquitectura de red** | Conjunto de protocolos compatibles entre sí | TCP/IP |
| **Interfaz** | Punto de conexión entre capas | Socket |
| **Servicio** | Lo que una capa ofrece a la de arriba | Entrega confiable |

### Las tres características de un protocolo

| Característica | Qué define | Ejemplo |
|---|---|---|
| **Sintaxis** | Formato de datos y niveles de señal | Campos de una trama |
| **Semántica** | Información de control y errores | ACK, NAK, códigos |
| **Temporización** | Coordinación de velocidades y secuencia | Timeouts, orden |

> [!warning] “Protocolo” no es “programa”
> Es un **conjunto de reglas**. La implementación es el software o hardware que las cumple.

## 1.3 Por qué normalizar

> [!quote] Cátedra
> **Normalización:** establecimiento de directrices que ordenan procedimientos y permiten aplicar reglas para una actividad determinada.

| Sin normalización | Con normalización |
|---|---|
| Cada fabricante inventa su formato | Interoperabilidad |
| No hay competencia real | Competencia por precio y calidad |
| Cambiar un equipo rompe todo | Sustitución por partes |

### Organismos

| Organismo | Ámbito | Ejemplo |
|---|---|---|
| **ISO** | Internacional, amplio | Modelo OSI |
| **IEEE** | Redes locales | IEEE 802.3 (Ethernet) |
| **ITU-T** | Telecomunicaciones | Recomendaciones de transmisión |
| **IETF** | Internet | RFC (IP, TCP, HTTP) |
| **W3C** | Web | HTML, CSS, XML |

> [!tip] En el oral
> “La normalización permite que equipos de distintos fabricantes interoperen. ISO define OSI; IEEE define las LAN; IETF define los protocolos de Internet mediante RFC.”

## 1.4 Clasificación de las comunicaciones

| Criterio | Tipos |
|---|---|
| Sentido | Simplex, semi-dúplex, dúplex |
| Señal | Analógica, digital |
| Medio | Guiado, no guiado |
| Alcance | PAN, LAN, MAN, WAN |
| Conmutación | Circuitos, paquetes |
| Difusión | Difusión, conmutada |

### Modos de transmisión

| Modo | Definición | Ejemplo |
|---|---|---|
| **Simplex** | Una estación siempre transmite, la otra siempre recibe | Radio, TV |
| **Semi-dúplex** | Alternan: uno transmite y luego el otro | Radioaficionados |
| **Dúplex (full)** | Ambos transmiten y reciben a la vez | Teléfono, Ethernet conmutada |

> [!important] La pregunta típica de UTN
> “Tipos de comunicaciones, características.” Respondé con los tres modos y un ejemplo de cada uno. En full-dúplex digital se usan **dos pares trenzados**; en analógico inalámbrico, **dos frecuencias**.

## 1.5 Método: analizar un sistema de comunicación

| Paso | Pregunta | Resultado |
|---|---|---|
| 1 | ¿Quién genera la información? | Fuente |
| 2 | ¿Cómo se convierte en señal? | Transductor |
| 3 | ¿Qué medio se usa? | Guiado o no guiado |
| 4 | ¿Qué protocolo gobierna? | Reglas |
| 5 | ¿Qué puede perturbarla? | Ruido, atenuación |
| 6 | ¿Cómo se recupera? | Receptor + transductor |

## Errores que suelen tomar

| Error | Corrección |
|---|---|
| Confundir protocolo con arquitectura | Protocolo = reglas; arquitectura = conjunto compatible |
| Decir que simplex es “un solo sentido físico” | Es un solo sentido lógico de transmisión |
| Creer que normalizar es “estandarizar la marca” | Es acordar reglas técnicas |
| Omitir la temporización | Es una de las tres características |
| Confundir transmisión de datos con comunicación | La primera es binaria y técnica |

## Ejercicios

> [!example]- 1. Elementos
> **Enunciado:** en una videollamada, identificá fuente, transductor y medio.
> **Solución:** fuente: cámara/micrófono; transductor: sensor CMOS y micrófono; medio: Internet (guiado/no guiado según el tramo).

> [!example]- 2. Protocolo
> **Enunciado:** nombrá las tres características y un ejemplo de cada una.
> **Solución:** sintaxis (formato de trama), semántica (ACK/error), temporización (timeout, secuencia).

> [!example]- 3. Modos
> **Enunciado:** ¿qué modo usa un “walkie-talkie”?
> **Solución:** semi-dúplex: alternan transmisión y recepción.

> [!example]- 4. Normalización
> **Enunciado:** ¿para qué sirve IEEE 802.3?
> **Solución:** para normalizar Ethernet (nivel físico y de enlace) y permitir interoperabilidad.

> [!example]- 5. a papel
> **Enunciado:** dibujá el sistema de comunicación con sus siete elementos.
> **Solución:** ver 1.1.

## Lo que sigue

[[cm02_modelo-osi|Modelo de referencia OSI]].

#libro4 #fundamentos
