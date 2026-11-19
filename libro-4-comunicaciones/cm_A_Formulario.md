---
tags: [efip, comunicaciones, formulario]
libro: 4
anexo: A
---

# A. Formulario

> [!info] Cómo usarlo
> Todas las fórmulas del libro, con unidades y un ejemplo resuelto. Si una fórmula no está acá, no se toma en el EFIP.

## A.1 Información

| Fórmula | Expresión | Unidad |
|---|---|---|
| Entropía | `H = −Σ p_i log2 p_i` | bits/símbolo |
| Entropía máxima | `H_max = log2 n` | bits/símbolo |
| Tasa de información | `R = r_s · H` | bps |
| Información de un evento | `I = −log2 p` | bits |

**Ejemplo:** `P(A)=0,5`, `P(B)=0,25`, `P(C)=0,25` → `H = 1,5 bits/símbolo`.

## A.2 Señales

| Fórmula | Expresión |
|---|---|
| Período | `T = 1/f` |
| Frecuencia | `f = 1/T` |
| Longitud de onda | `λ = v/f` |
| Velocidad de la luz | `v ≈ 3×10⁸ m/s` |

**Ejemplo:** `f = 2,4 GHz` → `λ = 3×10⁸ / 2,4×10⁹ = 0,125 m`.

## A.3 Decibeles

| Fórmula | Expresión |
|---|---|
| Ganancia/pérdida | `dB = 10 log10(P2/P1)` |
| Potencia absoluta | `dBm = 10 log10(P/1 mW)` |
| dB a lineal | `P2/P1 = 10^(dB/10)` |
| dBm a mW | `P = 10^(dBm/10) mW` |

| Regla | Equivalencia |
|---|---|
| ×2 | +3 dB |
| ×10 | +10 dB |
| ×100 | +20 dB |
| ÷2 | −3 dB |
| ÷10 | −10 dB |

**Ejemplo:** `P = 100 mW` → `10 log10 100 = 20 dBm`.

## A.4 Capacidad

| Teorema | Fórmula | Condición |
|---|---|---|
| **Nyquist** | `C = 2B log2 M` | Canal **sin** ruido |
| **Shannon** | `C = B log2(1 + S/N)` | Canal **con** ruido |
| SNR en dB a lineal | `S/N = 10^(SNR_dB/10)` | — |
| Bits por símbolo | `bps = baudios · log2 M` | — |

**Ejemplo Nyquist:** `B = 3 kHz`, `M = 4` → `C = 2·3000·2 = 12.000 bps`.
**Ejemplo Shannon:** `B = 1 MHz`, `S/N = 63` → `C = 10⁶·log2 64 = 6 Mbps`.

## A.5 Muestreo y PCM

| Fórmula | Expresión |
|---|---|
| Nyquist (muestreo) | `fs ≥ 2 · fmax` |
| Tasa PCM | `R = fs · n_bits` |
| Voz telefónica | `8000 × 8 = 64 kbps` |

**Ejemplo:** señal de 4 kHz → `fs ≥ 8000 Hz`.

## A.6 Tramas

| Concepto | Valor |
|---|---|
| Trama Ethernet mínima | 64 bytes |
| Datos mínimos | 46 bytes |
| Trama Ethernet máxima | 1518 bytes |
| Con VLAN | 1522 bytes |
| FCS | 4 bytes |
| MAC | 6 bytes (48 bits) |
| Cabecera UDP | 8 bytes |
| Etiqueta MPLS | 4 bytes |

## A.7 Direccionamiento IP

| Fórmula | Expresión |
|---|---|
| Hosts útiles | `2^h − 2` |
| Bits de subred necesarios | `2^n ≥ subredes` |
| Tamaño de bloque | `256 − valor del octeto de máscara` |
| Broadcast | `red + bloque − 1` |
| Primer host | `red + 1` |
| Último host | `broadcast − 1` |

### Prefijos

| Prefijo | Máscara | Bloque | Hosts |
|---|---|---|---|
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |

### VLSM: bits según hosts

| Hosts | Bits | Prefijo |
|---|---|---|
| 2 | 2 | /30 |
| 6 | 3 | /29 |
| 14 | 4 | /28 |
| 30 | 5 | /27 |
| 62 | 6 | /26 |
| 126 | 7 | /25 |
| 254 | 8 | /24 |
| 510 | 9 | /23 |
| 1022 | 10 | /22 |

## A.8 Enrutamiento

| Protocolo | Tipo | Métrica | Transporte | Límite |
|---|---|---|---|---|
| RIP | Distancia-vector | Saltos | UDP 520 | 15 saltos |
| OSPF | Estado de enlace | Costo | IP 89 | Áreas |
| BGP | Path-vector | Atributos | TCP 179 | Políticas |

**Costo OSPF:** `costo = 10^8 / ancho de banda (bps)`.

**Regla de selección:** primero *longest match*; después, métrica entre rutas del mismo prefijo.

## A.9 TCP

| Fórmula | Expresión |
|---|---|
| Ventana efectiva | `min(cwnd, ventana anunciada)` |
| Slow start | `cwnd` se duplica por RTT |
| Congestion avoidance | `+1 MSS` por RTT |
| Tras timeout | `ssthresh = cwnd/2`, `cwnd = 1` |
| Tras 3 ACK dup | `ssthresh = cwnd/2`, `cwnd = ssthresh` |

## A.10 Última milla

| Tecnología | Medio | Velocidad típica | Distancia |
|---|---|---|---|
| ADSL | Cobre | 8/1 Mbps | ~3 km |
| VDSL | Cobre | 100 Mbps | ~500 m |
| HFC | Fibra + coaxial | Cientos de Mbps | Nodo |
| FTTH | Fibra | Gbps | km |

## A.11 Tabla de unidades

| Magnitud | Unidad |
|---|---|
| Frecuencia | Hz |
| Ancho de banda | Hz |
| Tasa de bits | bps |
| Velocidad de símbolo | baudios |
| Potencia | W, mW, dBm |
| Relación | dB |
| Información | bits, bits/símbolo |

> [!warning] Los tres errores de unidades
> 1. Usar Hz donde va bps (o al revés).
> 2. Usar `log10` donde va `log2`.
> 3. Olvidar pasar de kbps a bps antes de operar.

#libro4 #formulario
