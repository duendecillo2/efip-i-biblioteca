---
tags: [efip, comunicaciones, anexo, mapa]
libro: 4
anexo: D
---

# D. Mapa del programa y trazabilidad — Comunicaciones

> [!info] Para qué sirve
> Ver qué sub-eje cubre cada capítulo, de qué documento sale y qué quedó afuera.

## D.1 Cobertura del programa

| Sub-eje oficial | Capítulos | Estado |
|---|---|---|
| **6.1** Sistemas de comunicaciones: modelo OSI, arquitectura TCP/IP, medida de la información y señales | [[cm01_sistemas-de-comunicacion\|1]] · [[cm02_modelo-osi\|2]] · [[cm03_tcp-ip\|3]] · [[cm04_informacion-y-senales\|4]] | ✅ Completo |
| **6.2** Estructura física: transmisión, perturbaciones, codificación, modulación, medios, última milla | [[cm05_transmision-y-perturbaciones\|5]] · [[cm06_codificacion-y-modulacion\|6]] · [[cm07_medios-y-dispositivos\|7]] · [[cm08_ultima-milla\|8]] | ✅ Completo |
| **6.3** Enlace de datos: funciones, PDU, protocolos, IEEE 802.x | [[cm09_nivel-enlace\|9]] · [[cm10_protocolos-bit\|10]] · [[cm11_llc-mac-802\|11]] | ✅ Completo |
| **6.4** Redes: topologías, direccionamiento, enrutamiento, congestión, WAN/MPLS, móviles | [[cm12_redes-y-topologias\|12]] · [[cm13_direccionamiento-ip\|13]] · [[cm14_enrutamiento\|14]] · [[cm15_tcp-udp-congestion\|15]] · [[cm16_wan-mpls-moviles\|16]] | ✅ Completo |

## D.2 Fuente de cada bloque

| Bloque | Base Siglo 21 | Complemento |
|---|---|---|
| 6.1 | `EFIP_BASE_S21/6.1_OSI_TCPIP_y_senales/` — lecturas de INF395 | **UTN Comunicaciones**: resúmenes 1–3, `Preguntas Tipicas.pdf` (NRZ, dBm, AB, ruido, modulación). **UP**: módulos de introducción a redes |
| 6.2 | `EFIP_BASE_S21/6.2_Estructura_fisica/` | **UTN Comunicaciones**: `Resumen Libro Ludueña.pdf`, TP1–TP3 resueltos (PCM, capacidad, medios). **UNLP**: apuntes de nivel físico |
| 6.3 | `EFIP_BASE_S21/6.3_Enlace_de_datos/` (ficha con vocabulario de PDU/SDU/PCI) | **UTN Comunicaciones**: control de paridad VRC/LRC, HDLC, PPP. **UTN Redes**: Ethernet y 802.3 |
| 6.4 | `EFIP_BASE_S21/6.4_Redes_y_enrutamiento/` | **UTN Redes de Información**: `redes_enorden` (RIP/OSPF/BGP/subnetting), `redes_resumen` (topologías, WAN, congestión), `redes_resumen1` (1er parcial) |
| Anexos | — | Consolidación propia a partir de los cuatro sub-ejes |

> [!important] El método es de UTN
> - **Subnetting y VLSM:** método del bloque (`256 − máscara`) y asignación de mayor a menor.
> - **Enrutamiento:** RIP (UDP 520, 30 s, 15 saltos), OSPF (áreas, costo, IP 89), BGP (path-vector, TCP 179, AS_PATH).
> - **Congestión:** slow start, AIMD, fast retransmit.
> - **Preguntas de oral:** el banco del anexo B sigue el formato de `Preguntas Tipicas.pdf` de UTN.

## D.3 Qué quedó fuera y por qué

| Tema | Motivo |
|---|---|
| Cálculo detallado de CRC por división polinómica | El EFIP pide el concepto; el cálculo completo es de UTN y se resolvió en el Libro 1 (operaciones binarias) |
| Codificación 8b/10b, 4B/5B, scrambling | Fuera del programa S21; se mencionan solo como elección de estándar |
| Wi-Fi 6/7 a nivel de capa física (OFDMA, MU-MIMO) | Solo tendencia; el programa pide 802.11 a nivel de acceso al medio |
| Detalle de señalización celular (RRC, NAS) | Fuera de alcance; se cubren handoff, roaming y generaciones |
| Configuración de equipos (Cisco IOS) | El EFIP es conceptual; los comandos se citan solo como método de diagnóstico |
| Cálculo de tráfico telefónico (Erlang) | No está en el programa de Comunicaciones |

## D.4 Enlaces con los otros libros

| Tema de este libro | Se profundiza en |
|---|---|
| Operaciones binarias y AND para máscaras | [[00_Inicio\|Libro 1 — Programación]] (sistemas de numeración) |
| Almacenamiento y consultas de datos | [[bd01_motores-de-bd\|Libro 2 — Base de Datos]] |
| Documentación de arquitectura de red | [[ad16_arquitectura\|Libro 3 — Análisis y Diseño]] |
| Caso integrador del municipio | [[00_Inicio_CM\|Presentación del libro]] |

## D.5 Plan de estudio sugerido

| Día | Qué | Archivos |
|---|---|---|
| 1 | Fundamentos y modelo | cap. 1–3 + cierre P1 |
| 2 | Información y señales | cap. 4 |
| 3 | Transmisión y capacidad | cap. 5 |
| 4 | Codificación y modulación | cap. 6 |
| 5 | Medios y última milla | cap. 7–8 + cierre P2 |
| 6 | Enlace y protocolos | cap. 9–11 + cierre P3 |
| 7 | Redes y direccionamiento | cap. 12–13 |
| 8 | Enrutamiento | cap. 14 |
| 9 | Transporte y congestión | cap. 15 |
| 10 | WAN, MPLS y móviles | cap. 16 + cierre P4 |
| 11 | Repaso | anexos A y C |
| 12 | Simulacro oral | anexo B completo |

> [!tip] Cómo rendir el oral
> 1. Ubicá la pregunta en la capa y en el sub-eje.
> 2. Definí con la frase de cátedra.
> 3. Agregá un ejemplo o una comparación.
> 4. Cerrá con la consecuencia práctica ("por eso se usa…").

#libro4 #mapa
