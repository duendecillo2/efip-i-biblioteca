---
tags: [efip, comunicaciones, cierre]
libro: 4
parte: 3
---

# Cierre de la Parte 3 — Enlace de datos

> [!info] Qué hacer con este archivo
> Verificación de 6.3. Si algo falla, volvé a los capítulos 9 a 11.

## Checklist de la Parte 3

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Enumerar las funciones de la capa 2 | [[cm09_nivel-enlace\|Cap. 9]] | ☐ |
| Explicar PDU, SDU y PCI | [[cm09_nivel-enlace\|Cap. 9]] | ☐ |
| Explicar entramado y bit stuffing | [[cm09_nivel-enlace\|Cap. 9]] | ☐ |
| Diferenciar paridad, checksum y CRC | [[cm09_nivel-enlace\|Cap. 9]] | ☐ |
| Describir ARQ y ventana | [[cm09_nivel-enlace\|Cap. 9]] | ☐ |
| Dibujar la trama HDLC | [[cm10_protocolos-bit\|Cap. 10]] | ☐ |
| Explicar LCP, NCP y PAP/CHAP | [[cm10_protocolos-bit\|Cap. 10]] | ☐ |
| Diferenciar LLC de MAC | [[cm11_llc-mac-802\|Cap. 11]] | ☐ |
| Leer la trama Ethernet y sus tamaños | [[cm11_llc-mac-802\|Cap. 11]] | ☐ |
| Explicar CSMA/CD y CSMA/CA | [[cm11_llc-mac-802\|Cap. 11]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| SDU | PDU | Datos del servicio vs. datos + control |
| HDLC | PPP | Confiable con ARQ vs. detecta y descarta |
| LLC | MAC | Interfaz con la red vs. acceso al medio |
| CSMA/CD | CSMA/CA | Detecta colisión vs. la evita |
| Switch | Hub | Capa 2 (MAC) vs. capa 1 (repite) |
| Trama mínima | Datos mínimos | 64 bytes vs. 46 bytes |
| Paridad | CRC | Baja detección vs. alta detección |

## Ejercicio integrador de la Parte 3

> [!example] Enunciado (20 minutos)
> 1. ¿Qué campos tiene una trama HDLC y para qué sirve cada uno?
> 2. ¿Por qué PPP no garantiza entrega?
> 3. Una trama Ethernet tiene 40 bytes de datos. ¿Qué pasa?
> 4. Explicá la diferencia entre LLC y MAC con un ejemplo.

> [!success]- Solución
> **1.** Bandera (delimita), dirección (estación), control (tipo, secuencia, ACK), datos, FCS (CRC) y bandera final.
> **2.** Porque detecta errores con FCS y descarta la trama; no retransmite. La confiabilidad la aporta TCP.
> **3.** Se rellena con padding hasta 46 bytes de datos para alcanzar la trama mínima de 64.
> **4.** LLC ofrece una interfaz común a IP; MAC resuelve el acceso y el direccionamiento del medio (Ethernet o Wi-Fi).

## Oral de la Parte 3 (8 preguntas)

> [!question]- 1. ¿Qué hace la capa de enlace?
> Entrama, direcciona físicamente, detecta errores, controla el flujo y el acceso al medio.

> [!question]- 2. ¿Qué es una PDU?
> La unidad de datos del protocolo: SDU + PCI.

> [!question]- 3. ¿Qué es el bit stuffing?
> Insertar un 0 tras cinco 1 consecutivos para que la bandera no aparezca en los datos.

> [!question]- 4. ¿CRC corrige errores?
> No: detecta. La corrección se hace por retransmisión o FEC.

> [!question]- 5. ¿Qué diferencia hay entre HDLC y PPP?
> HDLC es confiable y orientado a conexión; PPP encapsula, autentica y delega la confiabilidad.

> [!question]- 6. ¿Qué hace LLC?
> Multiplexa protocolos de red y ofrece una interfaz independiente del medio.

> [!question]- 7. ¿Por qué Ethernet tiene un mínimo de 64 bytes?
> Para detectar colisiones antes de terminar la transmisión.

> [!question]- 8. ¿Por qué Wi-Fi usa CSMA/CA?
> Porque no puede escuchar mientras transmite; evita colisiones con espera y ACK.

## Lo que sigue

[[cm12_redes-y-topologias|Redes, conmutación y topologías]].

#libro4 #cierre #enlace
