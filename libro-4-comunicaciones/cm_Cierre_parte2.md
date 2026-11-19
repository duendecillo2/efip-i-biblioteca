---
tags: [efip, comunicaciones, cierre]
libro: 4
parte: 2
---

# Cierre de la Parte 2 — Estructura física

> [!info] Qué hacer con este archivo
> Verificación de 6.2. Si algo falla, volvé a los capítulos 5 a 8.

## Checklist de la Parte 2

| Puedo… | Capítulo | ✔ |
|---|---|---|
| Distinguir frecuencia, espectro y ancho de banda | [[cm05_transmision-y-perturbaciones\|Cap. 5]] | ☐ |
| Calcular dB y dBm | [[cm05_transmision-y-perturbaciones\|Cap. 5]] | ☐ |
| Explicar atenuación, distorsión y ruido | [[cm05_transmision-y-perturbaciones\|Cap. 5]] | ☐ |
| Aplicar Nyquist y Shannon | [[cm05_transmision-y-perturbaciones\|Cap. 5]] | ☐ |
| Dibujar NRZ-L, NRZ-I y Manchester | [[cm06_codificacion-y-modulacion\|Cap. 6]] | ☐ |
| Distinguir ASK, FSK, PSK y QAM | [[cm06_codificacion-y-modulacion\|Cap. 6]] | ☐ |
| Explicar PCM y 64 kbps | [[cm06_codificacion-y-modulacion\|Cap. 6]] | ☐ |
| Comparar UTP, coaxial y fibra | [[cm07_medios-y-dispositivos\|Cap. 7]] | ☐ |
| Elegir medio por distancia y ruido | [[cm07_medios-y-dispositivos\|Cap. 7]] | ☐ |
| Explicar xDSL, HFC y FTTH | [[cm08_ultima-milla\|Cap. 8]] | ☐ |

## Diferencias que no podés confundir

| A | B | Diferencia central |
|---|---|---|
| Ancho de banda | Tasa de bits | Hz vs. bps |
| Atenuación | Distorsión de retardo | Pérdida de potencia vs. dispersión temporal |
| Ruido térmico | Ruido impulsivo | Continuo y de fondo vs. picos |
| Nyquist | Shannon | Sin ruido vs. con ruido |
| NRZ | Manchester | Sin transición obligatoria vs. autosincronizado |
| AM | ASK | Analógica vs. digital sobre portadora |
| UTP | Fibra | Cobre, 100 m vs. vidrio, km |
| xDSL | FTTH | Cobre vs. fibra hasta el hogar |

## Ejercicio integrador de la Parte 2

> [!example] Enunciado (25 minutos)
> 1. Un enlace de 100 m en una oficina con PCs. ¿Qué medio y por qué?
> 2. Si `B = 2 kHz` y `M = 4`, ¿capacidad según Nyquist?
> 3. Si `B = 1 MHz` y `SNR = 20 dB`, ¿capacidad según Shannon?
> 4. Explicá por qué no conviene usar 256-QAM en un enlace con mucho ruido.

> [!success]- Solución
> **1.** UTP Cat 5e/6: cubre 100 m, es económico y suficiente.
> **2.** `C = 2·2000·log2 4 = 8000 bps`.
> **3.** `S/N = 10^(20/10) = 100`; `C = 10^6·log2(101) ≈ 6,66 Mbps`.
> **4.** Porque con 256 niveles los puntos de la constelación están muy próximos y el ruido los confunde; el BER sube. Conviene una modulación más robusta (QPSK/FSK) o mejorar la SNR.

## Oral de la Parte 2 (8 preguntas)

> [!question]- 1. ¿Qué es el ancho de banda?
> El rango de frecuencias donde se concentra la mayor parte de la energía de la señal.

> [!question]- 2. ¿Qué es la atenuación?
> La pérdida de potencia de la señal al propagarse por el medio.

> [!question]- 3. ¿Qué es el ruido térmico?
> El producido por la agitación de electrones; depende de la temperatura, es uniforme en el espectro y no se elimina.

> [!question]- 4. ¿Qué es la distorsión de retardo?
> El ensanchamiento temporal porque la velocidad de propagación varía con la frecuencia.

> [!question]- 5. NRZ vs. Manchester.
> NRZ no garantiza transiciones; Manchester tiene una transición por bit y es autosincronizado, a costa del doble de AB.

> [!question]- 6. ¿Qué modula QAM?
> Amplitud y fase a la vez.

> [!question]- 7. ¿Qué es PCM?
> Digitalización por muestreo, cuantización y codificación. Voz: 8 kHz × 8 bits = 64 kbps.

> [!question]- 8. ¿Qué es la última milla?
> El tramo entre el usuario final y el operador; concentra costo y dificultad de cobertura.

## Lo que sigue

[[cm09_nivel-enlace|Nivel 2: funciones, PDU y entramado]].

#libro4 #cierre #transmision
