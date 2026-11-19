---
tags: [efip, comunicaciones, errores]
libro: 4
anexo: C
---

# C. Errores frecuentes

> [!info] Cómo usarlo
> Antes del examen, leé solo esta tabla. La columna derecha es lo que hay que decir.

## C.1 Modelo y capas

| Error | Corrección |
|---|---|
| "OSI es un protocolo" | Es un modelo de referencia de 7 capas |
| "OSI tiene 5 capas" | 7: física, enlace, red, transporte, sesión, presentación, aplicación |
| "TCP/IP tiene 7 capas" | 4: acceso a la red, internet, transporte, aplicación |
| "El switch es capa 3" | Capa 2 (MAC); solo el switch capa 3 enruta |
| "El router arma tramas" | Arma paquetes; la trama es capa 2 |
| "TCP es capa de red" | Es transporte |
| "HTTP es presentación" | Es aplicación |
| "La MAC llega de extremo a extremo" | Cambia en cada salto |
| "ARP es capa 3 pura" | Puentea red y enlace (2/3) |
| "IP es confiable" | Es *best effort*; TCP aporta confiabilidad |

## C.2 Información y señales

| Error | Corrección |
|---|---|
| Calcular entropía con `log10` | Es `log2` |
| "Más probabilidad = más información" | Al revés: lo improbable informa más |
| Confundir entropía con tasa | `H` es por símbolo; `R = r_s · H` es por segundo |
| Muestrear con `fs = fmax` | Debe ser `fs ≥ 2·fmax` |
| Confundir baudios con bps | `bps = baudios · log2 M` |
| Decir que PCM usa 4 kHz | Se muestrea a 8 kHz |

## C.3 Transmisión

| Error | Corrección |
|---|---|
| Confundir ancho de banda con tasa | Hz vs. bps |
| Usar `log10` en Shannon | Es `log2` |
| Olvidar convertir dB a lineal | `S/N = 10^(dB/10)` |
| "El ruido térmico se elimina" | No se elimina: limita la capacidad |
| Confundir diafonía con ruido térmico | La diafonía viene de otro par |
| "Más ancho de banda = más velocidad siempre" | Depende del ruido y del overhead |
| "dBm negativo = potencia negativa" | Es potencia menor que 1 mW |

## C.4 Codificación y medios

| Error | Corrección |
|---|---|
| "NRZ es autosincronizado" | Manchester lo es |
| Confundir NRZ-L con NRZ-I | L = nivel; I = transición en cada 1 |
| "Manchester usa menos AB" | Usa el doble |
| Confundir AM con ASK | AM es analógica; ASK es digital sobre portadora |
| "UTP llega a 1 km" | 100 m |
| Confundir fibra multimodo con monomodo | Multimodo: media distancia; monomodo: larga |
| "El hub es capa 2" | Capa 1 |
| "Inalámbrico = sin medio" | El aire es el medio |
| "ADSL es simétrico" | Es asimétrico |

## C.5 Enlace

| Error | Corrección |
|---|---|
| Confundir PDU con SDU | `PDU = SDU + PCI` |
| "La capa 2 comunica extremos" | Comunica nodos vecinos |
| "CRC corrige errores" | Detecta; se corrige por retransmisión o FEC |
| Bit stuffing con bytes | Es con bits; con caracteres es byte stuffing |
| Confundir control de flujo con acceso al medio | Receptor vs. canal |
| "La paridad detecta todo" | Solo detecta un número impar de errores simples |
| "HDLC es orientado al carácter" | Es orientado al bit |
| "PPP corrige errores" | Detecta y descarta |
| Confundir LCP con NCP | Enlace vs. protocolo de red |
| "MAC de 32 bits" | 48 bits |
| "La MAC se enruta" | Se conmuta dentro del segmento |
| "Ethernet mínimo 46 bytes" | La trama mínima es 64 (datos 46) |
| "CSMA/CA detecta colisiones" | Las evita |

## C.6 Redes

| Error | Corrección |
|---|---|
| Confundir topología física con lógica | Planos distintos |
| "La conmutación de circuitos es más eficiente" | Reserva capacidad y puede desperdiciarla |
| "Un hub segmenta" | Repite; no segmenta |
| Restar 2 en `/31` | En `/31` hay 2 hosts válidos |
| Confundir dirección de red con primer host | Red = `.0` del bloque |
| "`172.16.0.0/8` es la privada B" | Es `/12` |
| Sumarizar redes no contiguas | Deben ser contiguas y alineadas |
| En VLSM empezar por la subred chica | Empezar por la más grande |
| "IPv6 tiene broadcast" | Usa multicast |
| Usar `::` dos veces en IPv6 | Solo una vez |

## C.7 Enrutamiento

| Error | Corrección |
|---|---|
| Confundir enrutado con de enrutamiento | Datos vs. rutas |
| "RIP elige la ruta más rápida" | Elige la de menos saltos |
| "RIP soporta 16 saltos" | Máximo 15; 16 = inalcanzable |
| "OSPF usa UDP" | Va sobre IP, protocolo 89 |
| "BGP elige el camino más corto" | Aplica atributos y políticas |
| Comparar métricas de distinto prefijo | Primero longest match |
| "OSPF no tiene jerarquía" | Usa áreas con área 0 |
| "El ruteo estático se adapta" | No se adapta a fallas |

## C.8 Transporte

| Error | Corrección |
|---|---|
| Confundir control de flujo con congestión | Receptor vs. red |
| "Slow start es lineal" | Es exponencial |
| "TCP siempre reduce a 1 la ventana" | Solo ante timeout; con ACK dup baja a la mitad |
| "UDP es siempre más rápido" | Menos overhead, sin garantías |
| Confundir ACK con bytes recibidos | Es el próximo byte esperado |
| "El handshake es de 2 mensajes" | Son 3 |
| "El cierre es de 2 pasos" | Es de 4 (full-duplex) |
| "QoS agrega ancho de banda" | Solo lo administra |

## C.9 WAN y móviles

| Error | Corrección |
|---|---|
| "MPLS es un protocolo de enrutamiento" | Es una técnica de conmutación por etiquetas |
| "MPLS reemplaza a IP" | Transporta paquetes IP |
| Confundir LER con LSR | Borde vs. núcleo |
| "Handoff es roaming" | Celda vs. otra red de operador |
| "5G es solo 4G más rápido" | Agrega URLLC, mMTC y slicing |
| "VPN es una línea privada" | Es un túnel cifrado sobre red pública |
| "Frame Relay sigue vigente" | Está obsoleto |

## C.10 Los cinco errores que más cuestan puntos

> [!warning] Si tenés poco tiempo, memorizá estos cinco
> 1. **Hz ≠ bps** (ancho de banda vs. tasa).
> 2. **`log2`, no `log10`** en entropía, Nyquist y Shannon.
> 3. **PDU = SDU + PCI** y cada capa tiene su PDU.
> 4. **RIP = saltos (15 máx.)**, **OSPF = costo**, **BGP = políticas**.
> 5. **Longest match antes que métrica** en la tabla de ruteo.

#libro4 #errores
