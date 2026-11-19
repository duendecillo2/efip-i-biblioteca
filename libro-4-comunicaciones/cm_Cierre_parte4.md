---
tags: [efip, comunicaciones, cierre]
libro: 4
parte: 4
---

# Cierre de la Parte 4 — Redes

> [!info] Qué hacer con este archivo
> Verificación de 6.4. Si algo falla, volvé a los capítulos 12 a 16.

## Checklist de la Parte 4

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Distinguir red de difusión de conmutada | [[cm12_redes-y-topologias\|Cap. 12]] | ☐ |
| Comparar conmutación de circuitos y paquetes | [[cm12_redes-y-topologias\|Cap. 12]] | ☐ |
| Nombrar topologías y su diferencia física/lógica | [[cm12_redes-y-topologias\|Cap. 12]] | ☐ |
| Describir una LAN, sus dominios y VLAN | [[cm12_redes-y-topologias\|Cap. 12]] | ☐ |
| Explicar la interconexión de redes (router, NAT, ARP) | [[cm12_redes-y-topologias\|Cap. 12]] | ☐ |
| Clasificar una IPv4 y reconocer privadas | [[cm13_direccionamiento-ip\|Cap. 13]] | ☐ |
| Calcular red, broadcast y rango de hosts | [[cm13_direccionamiento-ip\|Cap. 13]] | ☐ |
| Hacer subnetting y VLSM paso a paso | [[cm13_direccionamiento-ip\|Cap. 13]] | ☐ |
| Explicar CIDR y una IPv6 | [[cm13_direccionamiento-ip\|Cap. 13]] | ☐ |
| Diferenciar enrutado de de enrutamiento | [[cm14_enrutamiento\|Cap. 14]] | ☐ |
| Comparar RIP, OSPF y BGP | [[cm14_enrutamiento\|Cap. 14]] | ☐ |
| Explicar handshake, ventana y congestión | [[cm15_tcp-udp-congestion\|Cap. 15]] | ☐ |
| Decidir TCP vs. UDP con criterios | [[cm15_tcp-udp-congestion\|Cap. 15]] | ☐ |
| Explicar MPLS y sus beneficios | [[cm16_wan-mpls-moviles\|Cap. 16]] | ☐ |
| Diferenciar handoff de roaming | [[cm16_wan-mpls-moviles\|Cap. 16]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| Enrutado | De enrutamiento | Datos vs. rutas |
| RIP | OSPF | Saltos vs. costo; distancia-vector vs. estado de enlace |
| OSPF | BGP | Interior vs. entre AS |
| Conmutación de circuitos | De paquetes | Camino reservado vs. almacenar y reenviar |
| Control de flujo | Control de congestión | Receptor vs. red |
| TCP | UDP | Confiable vs. sin garantías |
| Subnetting | VLSM | Máscaras iguales vs. distintas |
| Handoff | Roaming | Cambio de celda vs. otra red |
| MPLS | IP | Etiqueta vs. dirección destino |

## Ejercicio integrador de la Parte 4

> [!example] Enunciado (30 minutos)
> El municipio tiene tres sedes con 300, 120 y 40 hosts, y necesita conectar los semáforos.
> 1. Partí `10.10.0.0/16` con VLSM para las tres sedes.
> 2. ¿Qué protocolo de enrutamiento usarías entre sedes y por qué?
> 3. El centro de monitoreo recibe video. ¿TCP o UDP? ¿Por qué?
> 4. ¿Qué tecnología WAN propondrías con QoS y por qué?

> [!success]- Solución
> **1.** 300 → `/23` (`10.10.0.0/23`, 510 hosts); 120 → `/25` (`10.10.2.0/25`, 126); 40 → `/26` (`10.10.2.128/26`, 62). Orden: de mayor a menor.
> **2.** **OSPF**: hay más de 15 saltos potenciales, conviene métrica por costo y convergencia rápida; además permite áreas.
> **3.** **UDP** para el video en vivo (latencia sobre pérdida); **TCP** si el video se descarga o debe verse sin artefactos.
> **4.** **MPLS** (o SD-WAN con QoS): permite priorizar video y voz, garantizar SLA y separar tráfico por etiquetas.

## Oral de la Parte 4 (10 preguntas)

> [!question]- 1. ¿Qué es una red conmutada?
> Una red donde nodos interconectados encaminan la información entre origen y destino, a diferencia de la difusión, donde todos comparten el medio.

> [!question]- 2. ¿Qué es subnetting?
> Subdividir una red IP en varias subredes tomando bits de la porción de host.

> [!question]- 3. ¿Cuántos hosts tiene un `/27`?
> 30 útiles: `2^5 − 2`.

> [!question]- 4. ¿Qué es VLSM?
> Usar máscaras de distinta longitud según la necesidad de cada subred, asignando de mayor a menor.

> [!question]- 5. Protocolo enrutado vs. de enrutamiento.
> El enrutado transporta datos (IP); el de enrutamiento intercambia rutas (RIP, OSPF, BGP).

> [!question]- 6. RIP: métrica y límite.
> Saltos; máximo 15 (16 = inalcanzable), UDP 520, actualiza cada 30 s.

> [!question]- 7. OSPF: métrica y por qué usa áreas.
> Costo (según ancho de banda); las áreas limitan el tamaño de la LSDB y mejoran la convergencia.

> [!question]- 8. TCP: three-way handshake.
> SYN → SYN-ACK → ACK; sincroniza los números iniciales de secuencia.

> [!question]- 9. Slow start vs. congestion avoidance.
> Slow start crece exponencialmente; avoidance crece lineal (+1 MSS por RTT) tras `ssthresh`.

> [!question]- 10. MPLS: qué es un LSP.
> El camino conmutado por etiquetas que sigue un flujo desde el LER de ingreso hasta el de egreso.

## Cierre del libro

> [!success] Si podés responder todo esto
> Cubriste los cuatro sub-ejes del Módulo 4: modelo de referencia y señales (6.1), estructura física (6.2), enlace de datos (6.3) y redes (6.4).
> Seguí con el [[cm_B_Banco_preguntas|banco de preguntas]] y el [[cm_A_Formulario|formulario]].

## Lo que sigue

[[cm_A_Formulario|A. Formulario]].

#libro4 #cierre #redes
