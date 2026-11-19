---
tags: [efip, comunicaciones, cierre]
libro: 4
parte: 1
---

# Cierre de la Parte 1 — Fundamentos y modelo de referencia

> [!info] Qué hacer con este archivo
> Verificación de 6.1. Si algo falla, volvé a los capítulos 1 a 4.

## Checklist de la Parte 1

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Nombrar los elementos de un sistema de comunicación | [[cm01_sistemas-de-comunicacion\|Cap. 1]] | ☐ |
| Explicar protocolo, arquitectura y normalización | [[cm01_sistemas-de-comunicacion\|Cap. 1]] | ☐ |
| Nombrar las siete capas de OSI y su función | [[cm02_modelo-osi\|Cap. 2]] | ☐ |
| Asociar PDU y dispositivos a cada capa | [[cm02_modelo-osi\|Cap. 2]] | ☐ |
| Mapear TCP/IP contra OSI | [[cm03_tcp-ip\|Cap. 3]] | ☐ |
| Explicar el encapsulamiento | [[cm03_tcp-ip\|Cap. 3]] | ☐ |
| Calcular entropía y tasa de información | [[cm04_informacion-y-senales\|Cap. 4]] | ☐ |
| Explicar muestreo y PCM (64 kbps) | [[cm04_informacion-y-senales\|Cap. 4]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| Modelo OSI | Arquitectura TCP/IP | Referencia vs. implementación |
| Protocolo | Arquitectura | Reglas vs. conjunto compatible |
| Capa de red | Capa de transporte | Ruta entre redes vs. extremo a extremo |
| Switch | Router | Capa 2 (MAC) vs. capa 3 (IP) |
| Entropía | Tasa de información | Bits por símbolo vs. bits por segundo |
| Analógica | Digital | Continua vs. discreta |
| Baudios | bps | Símbolos/s vs. bits/s |

## Ejercicio integrador de la Parte 1

> [!example] Enunciado (20 minutos)
> 1. Ubicá: HTTP, TCP, IP, Ethernet y un hub en las capas OSI.
> 2. Calculá la entropía de una fuente con `P(A)=0,25`, `P(B)=0,25`, `P(C)=0,5`.
> 3. Si `r_s = 2000` símbolos/s, ¿cuál es la tasa?
> 4. ¿Qué frecuencia mínima de muestreo necesita una señal de 5 kHz?

> [!success]- Solución
> **1.** HTTP → aplicación (7); TCP → transporte (4); IP → red (3); Ethernet → enlace (2); hub → física (1).
> **2.** `H = -(0,25·(-2) + 0,25·(-2) + 0,5·(-1)) = 1,5 bits/símbolo`.
> **3.** `R = 2000 × 1,5 = 3000 bps`.
> **4.** `fs ≥ 2 × 5000 = 10 kHz`.

## Oral de la Parte 1 (8 preguntas)

> [!question]- 1. ¿Qué es un protocolo?
> Conjunto de reglas acordadas para intercambiar información, con sintaxis, semántica y temporización.

> [!question]- 2. ¿Por qué normalizar?
> Para que equipos de distintos fabricantes interoperen y se puedan sustituir por partes.

> [!question]- 3. ¿OSI es un protocolo?
> No: es un modelo de referencia de siete capas.

> [!question]- 4. Nombrá las capas de abajo hacia arriba.
> Física, enlace, red, transporte, sesión, presentación y aplicación.

> [!question]- 5. ¿Qué hace la capa de red?
> Direccionamiento lógico, encaminamiento y control de congestión entre redes.

> [!question]- 6. ¿Qué diferencia hay entre TCP e IP?
> IP entrega paquetes sin conexión ni confiabilidad; TCP establece conexión y garantiza entrega ordenada.

> [!question]- 7. ¿Qué es la entropía?
> La información media por símbolo de una fuente, medida en bits/símbolo.

> [!question]- 8. ¿Por qué se muestrea a 8 kHz en telefonía?
> Porque la voz llega a 4 kHz y Nyquist exige al menos el doble.

## Lo que sigue

[[cm05_transmision-y-perturbaciones|Transmisión: ancho de banda, perturbaciones y capacidad]].

#libro4 #cierre #fundamentos
