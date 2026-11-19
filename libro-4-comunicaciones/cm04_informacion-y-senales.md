---
tags: [efip, comunicaciones, informacion, senales]
libro: 4
capitulo: 4
subeje: "6.1"
---

# 4. Medida de la información y señales

> [!info] Al terminar este capítulo tenés que poder
> - Calcular entropía y tasa de información.
> - Distinguir señal analógica de digital.
> - Explicar muestreo, cuantización y codificación.
> - Aplicar el teorema de Nyquist para muestreo.

> [!abstract] Qué debés saber (nivel 1)
> - **Información** se vincula con la **incertidumbre**, no con el significado.
> - **Entropía:** bits por símbolo; máximo cuando los símbolos son equiprobables.
> - **Tasa de información:** símbolos por segundo × entropía.
> - **Señal analógica:** varía continuamente. **Digital:** discreta.
> - **Muestreo:** tomar valores a intervalos regulares.
> - **Nyquist (muestreo):** `fs ≥ 2 · fmax`.

## 4.1 Qué es información

> [!quote] Cátedra
> **Información:** aquello que se produce en la fuente para ser transferida, procesada, computada, distribuida o almacenada; se vincula con la **incertidumbre** y no con el significado del contenido.

Un mensaje predecible aporta poca información; uno improbable, mucha.

$$I(E) = \log_2 \frac{1}{P(E)} = -\log_2 P(E) \quad [\text{bits}]$$

> [!tip] La misma fórmula, dos usos
> Aplicada a un **evento** da la información de ese evento; promediada sobre todos los símbolos de una fuente da la **entropía**. Por eso `H` es la esperanza de `I(E)`.

| Evento | Probabilidad | Información |
|---|---|---|
| “Sale cara” en moneda honesta | 0,5 | 1 bit |
| “Sale 6” en dado | 1/6 | ≈ 2,58 bits |
| “Sale cara” en moneda con dos caras | 1 | 0 bits |

> [!important] La idea que se pregunta
> Cuanto más probable es un símbolo, **menos** información aporta. Si ya sabés lo que va a pasar, no te informa nada.

## 4.2 Entropía

$$H = -\sum_{i=1}^{n} p_i \log_2 p_i \quad [\text{bits/símbolo}]$$

### Ejemplo

Fuente con `P(A)=0,5`, `P(B)=0,25`, `P(C)=0,25`:

```text
H = -(0,5·log2 0,5 + 0,25·log2 0,25 + 0,25·log2 0,25)
H = -(0,5·(-1) + 0,25·(-2) + 0,25·(-2))
H = 0,5 + 0,5 + 0,5 = 1,5 bits/símbolo
```

| Caso | Entropía |
|---|---|
| Dos símbolos equiprobables | 1 bit/símbolo (máxima) |
| Cuatro equiprobables | 2 bits/símbolo |
| Un símbolo con probabilidad 1 | 0 bits/símbolo |

> [!tip] La cota
> La entropía máxima de una fuente con `n` símbolos es `log2 n`, y se alcanza cuando todos son equiprobables.

## 4.3 Tasa de información

$$R = r_s \cdot H \quad [\text{bits/s}]$$

- `r_s`: símbolos por segundo (velocidad de símbolo).
- `H`: bits por símbolo.

**Ejemplo:** `r_s = 1000 símbolos/s` y `H = 1,5` → `R = 1500 bps`.

> [!warning] No confundir
> **Velocidad de símbolo (baudios)** ≠ **velocidad de bits (bps)**. Si cada símbolo transporta más de un bit, los bps son mayores que los baudios.

| Magnitud | Unidad | Ojo |
|---|---|---|
| Información | bit | Se calcula con `log2` |
| Tasa de información | b/s | símbolos/s × bits/símbolo |
| Tamaño de archivo | byte (B) = 8 bits | `1 GB ≈ 8 Gb` |
| Tasa de un enlace | b/s (decimal) | `1 Mb/s = 10⁶ b/s`, no 2²⁰ |

**Ejemplo:** un archivo de 1 GB (≈ 8 Gb) sobre un enlace ideal de 100 Mb/s tarda como mínimo `8000/100 = 80 s`. En la práctica tarda más por cabeceras, control y congestión.

## 4.4 Señales

| | Analógica | Digital |
|---|---|---|
| Variación | Continua | Discreta |
| Forma | Onda suave | Pulsos |
| Ejemplo | Voz, temperatura | Datos binarios |
| Ventaja | Fiel al fenómeno | Robusta y regenerable |
| Desventaja | Se degrada con el ruido | Requiere más ancho de banda en banda base |

### Parámetros

| Parámetro | Qué es | Fórmula |
|---|---|---|
| **Amplitud** | Altura de la onda | — |
| **Frecuencia** | Ciclos por segundo | `f = 1/T` |
| **Período** | Duración de un ciclo | `T = 1/f` |
| **Fase** | Desplazamiento de la onda | — |
| **Longitud de onda** | Distancia de un ciclo | `λ = v/f` |

**Ejemplo:** `f = 100 MHz`, `v = 3×10⁸ m/s` → `λ = 3 m`.

> [!important] Tres formas de modular
> Se puede variar **amplitud (AM/ASK)**, **frecuencia (FM/FSK)** o **fase (PM/PSK)**. QAM combina amplitud y fase.

## 4.5 Muestreo y digitalización

Para transmitir una señal analógica por un canal digital se digitaliza:

```mermaid
flowchart LR
    A["Señal analógica"] --> M["Muestreo"]
    M --> C["Cuantización"]
    C --> E["Codificación"]
    E --> B["Bits"]
```

| Etapa | Qué hace |
|---|---|
| **Muestreo** | Toma valores a intervalos regulares |
| **Cuantización** | Asigna cada muestra a un nivel discreto |
| **Codificación** | Convierte el nivel en bits |

### Teorema de Nyquist (muestreo)

$$f_s \ge 2 \cdot f_{max}$$

**Ejemplo:** una señal de voz de hasta 4 kHz necesita `fs ≥ 8000 muestras/s`. Por eso la telefonía usa 8 kHz.

> [!warning] Si muestreás menos
> Se produce **aliasing**: la señal reconstruida es distinta de la original. No se arregla después con filtros.

### PCM

| Paso | Detalle |
|---|---|
| Muestreo | 8000 veces por segundo |
| Cuantización | 256 niveles (8 bits) |
| Tasa | `8000 × 8 = 64 kbps` |

> [!tip] El número que se pregunta
> Voz telefónica PCM: **64 kbps**. Sale de 8 kHz × 8 bits.

## 4.6 Método: resolver un problema de información

| Paso | Acción |
|---|---|
| 1 | Identificar símbolos y probabilidades |
| 2 | Calcular `H` con `-Σ p log2 p` |
| 3 | Verificar que `H ≤ log2 n` |
| 4 | Multiplicar por `r_s` para la tasa |
| 5 | Verificar unidades (bits/símbolo vs. bps) |

## Errores que suelen tomar

| Error | Corrección |
|---|---|
| Calcular entropía con `log10` | Es `log2` |
| Confundir entropía con tasa | `H` es por símbolo; la tasa es por segundo |
| Decir que más probabilidad = más información | Al revés |
| Muestrear con `fs = fmax` | Debe ser ≥ `2·fmax` |
| Confundir baudios con bps | Depende de bits por símbolo |
| Olvidar que la entropía máxima es `log2 n` | Usarlo como control |

## Ejercicios

> [!example]- 1. Entropía
> **Enunciado:** fuente binaria con `P(0)=0,9` y `P(1)=0,1`. ¿Entropía?
> **Solución:** `H = -(0,9 log2 0,9 + 0,1 log2 0,1) ≈ 0,469 bits/símbolo`.

> [!example]- 2. Tasa
> **Enunciado:** `r_s = 2400` y `H = 2` bits/símbolo.
> **Solución:** `R = 4800 bps`.

> [!example]- 3. Muestreo
> **Enunciado:** señal de 10 kHz. ¿Frecuencia mínima de muestreo?
> **Solución:** 20 kHz.

> [!example]- 4. PCM
> **Enunciado:** 8000 muestras/s con 8 bits. ¿Tasa?
> **Solución:** 64.000 bps = 64 kbps.

> [!example]- 5. Longitud de onda
> **Enunciado:** `f = 2,4 GHz`, `v = 3×10⁸ m/s`.
> **Solución:** `λ = 0,125 m` (12,5 cm).

> [!example]- 6. a papel
> **Enunciado:** explicá por qué una moneda honesta aporta 1 bit.
> **Solución:** porque hay dos resultados equiprobables y `H = log2 2 = 1` bit por símbolo.

## Lo que sigue

[[cm_Cierre_parte1|Cierre de la Parte 1]].

#libro4 #informacion #senales
