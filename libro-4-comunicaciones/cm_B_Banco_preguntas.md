---
tags: [efip, comunicaciones, preguntas]
libro: 4
anexo: B
---

# B. Banco de preguntas de oral

> [!info] Cómo usarlo
> Tapá la respuesta, contestá en voz alta en menos de un minuto y recién después desplegá. Si te trabás, el capítulo está al lado.

## B.1 Modelo de referencia (6.1)

> [!question]- 1. ¿Qué es un protocolo?
> Conjunto de reglas acordadas entre participantes para intercambiar información, con sintaxis, semántica y temporización. → [[cm01_sistemas-de-comunicacion|Cap. 1]]

> [!question]- 2. ¿Por qué es necesaria la normalización?
> Para que equipos de distintos fabricantes interoperen, se puedan sustituir por partes y exista competencia real. → [[cm01_sistemas-de-comunicacion|Cap. 1]]

> [!question]- 3. Diferenciá modelo de referencia y arquitectura.
> OSI es un modelo de referencia (qué debería hacer cada nivel); TCP/IP es la arquitectura implementada (protocolos concretos). → [[cm02_modelo-osi|Cap. 2]]

> [!question]- 4. Nombrá las siete capas y una función de cada una.
> Física (bits y medio), enlace (tramas y acceso), red (ruta), transporte (extremo a extremo), sesión (diálogo), presentación (formato y cifrado), aplicación (servicios). → [[cm02_modelo-osi|Cap. 2]]

> [!question]- 5. ¿Qué PDU corresponde a cada capa?
> Bit, trama, paquete, segmento, datos (de 1 a 7). → [[cm02_modelo-osi|Cap. 2]]

> [!question]- 6. ¿Qué hace el encapsulamiento?
> Cada capa agrega su cabecera de control; el receptor las quita en orden inverso. → [[cm03_tcp-ip|Cap. 3]]

> [!question]- 7. ¿Cuántas capas tiene TCP/IP y cómo se mapean?
> Cuatro: acceso a la red (física + enlace), internet (red), transporte y aplicación (aplicación + presentación + sesión). → [[cm03_tcp-ip|Cap. 3]]

> [!question]- 8. ¿Qué significa que IP no sea confiable?
> Que no confirma entrega ni orden: hace *best effort*. La confiabilidad la aporta TCP. → [[cm03_tcp-ip|Cap. 3]]

## B.2 Información y señales (6.1)

> [!question]- 9. ¿Qué es la entropía?
> La información media por símbolo de una fuente, medida en bits/símbolo. → [[cm04_informacion-y-senales|Cap. 4]]

> [!question]- 10. ¿Cuándo es máxima la entropía?
> Cuando todos los símbolos son equiprobables; vale `log2 n`. → [[cm04_informacion-y-senales|Cap. 4]]

> [!question]- 11. ¿Qué es el muestreo y qué teorema lo rige?
> Tomar valores a intervalos regulares; Nyquist exige `fs ≥ 2·fmax`. → [[cm04_informacion-y-senales|Cap. 4]]

> [!question]- 12. ¿Por qué la voz telefónica usa 64 kbps?
> Porque se muestrea a 8 kHz con 8 bits por muestra: `8000 × 8 = 64.000 bps`. → [[cm04_informacion-y-senales|Cap. 4]]

## B.3 Transmisión (6.2)

> [!question]- 13. ¿Qué es el ancho de banda?
> El rango de frecuencias donde se concentra la mayor parte de la energía de la señal, medido en Hz. → [[cm05_transmision-y-perturbaciones|Cap. 5]]

> [!question]- 14. ¿Qué es la atenuación y cómo se expresa?
> La pérdida de potencia al propagarse; se expresa en dB: `10 log10(P2/P1)`. → [[cm05_transmision-y-perturbaciones|Cap. 5]]

> [!question]- 15. Caracterizá el ruido térmico.
> Agitación de electrones; depende de la temperatura, es uniforme en el espectro y no se puede eliminar: limita la capacidad. → [[cm05_transmision-y-perturbaciones|Cap. 5]]

> [!question]- 16. ¿Qué es la distorsión de retardo?
> La dispersión temporal porque la velocidad de propagación varía con la frecuencia. → [[cm05_transmision-y-perturbaciones|Cap. 5]]

> [!question]- 17. Nyquist vs. Shannon.
> Nyquist vale sin ruido (`2B log2 M`); Shannon con ruido (`B log2(1+S/N)`). → [[cm05_transmision-y-perturbaciones|Cap. 5]]

> [!question]- 18. ¿Conviene usar muchos niveles de codificación?
> Sin ruido sí (aumenta la capacidad logarítmicamente); con ruido, los niveles se confunden y el BER sube. Se justifica con Shannon. → [[cm05_transmision-y-perturbaciones|Cap. 5]]

## B.4 Codificación y modulación (6.2)

> [!question]- 19. Explicá NRZ-L y NRZ-I.
> NRZ-L usa un nivel por bit; NRZ-I produce una transición en cada 1 y ninguna en 0. → [[cm06_codificacion-y-modulacion|Cap. 6]]

> [!question]- 20. ¿Por qué Manchester usa el doble de ancho de banda?
> Porque garantiza una transición en la mitad de cada bit, lo que duplica la frecuencia de cambio. → [[cm06_codificacion-y-modulacion|Cap. 6]]

> [!question]- 21. ¿Qué ventaja tiene Manchester diferencial?
> No depende de la polaridad: importa la presencia o ausencia de transición, no el nivel. → [[cm06_codificacion-y-modulacion|Cap. 6]]

> [!question]- 22. ¿Qué modula QAM?
> Amplitud y fase a la vez, lo que permite más bits por símbolo. → [[cm06_codificacion-y-modulacion|Cap. 6]]

> [!question]- 23. ¿Qué modulación ocupa menos ancho de banda?
> ASK (AM), porque solo varía la amplitud; FSK necesita más espectro. → [[cm06_codificacion-y-modulacion|Cap. 6]]

## B.5 Medios y última milla (6.2)

> [!question]- 24. Compará UTP, coaxial y fibra.
> UTP: barato, 100 m, sensible a ruido. Coaxial: mejor blindaje, rígido, en desuso en LAN. Fibra: km, inmune al ruido, más cara. → [[cm07_medios-y-dispositivos|Cap. 7]]

> [!question]- 25. Repetidor vs. amplificador.
> El amplificador amplifica también el ruido; el repetidor regenera la señal digital. → [[cm07_medios-y-dispositivos|Cap. 7]]

> [!question]- 26. ¿Qué medio elegirías para 80 m en una oficina?
> UTP Cat 5e/6: cubre 100 m, es económico y suficiente. → [[cm07_medios-y-dispositivos|Cap. 7]]

> [!question]- 27. ¿Qué es la última milla y por qué es crítica?
> El tramo entre el usuario y el operador; concentra el costo de obra y las limitaciones de distancia y compartición. → [[cm08_ultima-milla|Cap. 8]]

> [!question]- 28. Diferenciá xDSL, HFC y FTTH.
> xDSL usa cobre telefónico; HFC usa fibra hasta el nodo y coaxial hasta el hogar; FTTH lleva fibra hasta el domicilio. → [[cm08_ultima-milla|Cap. 8]]

## B.6 Enlace (6.3)

> [!question]- 29. ¿Qué es una PDU?
> La unidad de datos del protocolo: `PDU = SDU + PCI`. → [[cm09_nivel-enlace|Cap. 9]]

> [!question]- 30. ¿Qué es el bit stuffing y para qué se usa?
> Insertar un 0 tras cinco 1 consecutivos para que la bandera no aparezca en los datos. → [[cm09_nivel-enlace|Cap. 9]]

> [!question]- 31. ¿CRC corrige errores?
> No: detecta. La corrección se logra por retransmisión (ARQ) o FEC. → [[cm09_nivel-enlace|Cap. 9]]

> [!question]- 32. Diferenciá paridad VRC y LRC.
> VRC agrega un bit por carácter; LRC agrega un carácter de paridad al final del bloque. → [[cm09_nivel-enlace|Cap. 9]]

> [!question]- 33. Describí la trama HDLC.
> Bandera, dirección, control, datos, FCS y bandera; delimitación por `01111110` con relleno de bits. → [[cm10_protocolos-bit|Cap. 10]]

> [!question]- 34. ¿Qué diferencia hay entre HDLC y PPP?
> HDLC es confiable y orientado a conexión; PPP encapsula, autentica (PAP/CHAP) y no corrige errores. → [[cm10_protocolos-bit|Cap. 10]]

> [!question]- 35. ¿Qué hacen LCP y NCP en PPP?
> LCP negocia las opciones del enlace; NCP configura el protocolo de red (por ejemplo IPCP). → [[cm10_protocolos-bit|Cap. 10]]

> [!question]- 36. ¿Por qué la capa 2 se divide en LLC y MAC?
> LLC da independencia del medio e interfaz con la red; MAC resuelve direccionamiento y acceso al medio. → [[cm11_llc-mac-802|Cap. 11]]

> [!question]- 37. ¿Cuál es la trama mínima de Ethernet y por qué?
> 64 bytes (46 de datos + 18 de cabecera y FCS), para detectar colisiones antes de terminar de transmitir. → [[cm11_llc-mac-802|Cap. 11]]

> [!question]- 38. CSMA/CD vs. CSMA/CA.
> CD detecta colisiones (cable); CA las evita con espera aleatoria y ACK porque no puede escuchar mientras transmite (aire). → [[cm11_llc-mac-802|Cap. 11]]

## B.7 Redes (6.4)

> [!question]- 39. ¿Qué es una red de difusión?
> Una red donde todas las terminales comparten el medio y ven lo que se transmite. → [[cm12_redes-y-topologias|Cap. 12]]

> [!question]- 40. Conmutación de circuitos vs. paquetes.
> Circuitos reserva un camino exclusivo (retardo constante, capacidad desperdiciada); paquetes divide y encamina cada unidad (eficiente, retardo variable). → [[cm12_redes-y-topologias|Cap. 12]]

> [!question]- 41. ¿Qué separa un dominio de broadcast?
> Un router o una VLAN. → [[cm12_redes-y-topologias|Cap. 12]]

> [!question]- 42. ¿Cuántos hosts tiene un `/26`?
> 62: `2^6 − 2`. → [[cm13_direccionamiento-ip|Cap. 13]]

> [!question]- 43. ¿Cuáles son las rangos privados?
> `10.0.0.0/8`, `172.16.0.0/12` y `192.168.0.0/16`. → [[cm13_direccionamiento-ip|Cap. 13]]

> [!question]- 44. ¿Qué es VLSM?
> Usar máscaras de distinta longitud por subred, asignando de mayor a menor para no fragmentar el espacio. → [[cm13_direccionamiento-ip|Cap. 13]]

> [!question]- 45. ¿Qué es CIDR?
> El direccionamiento sin clases con prefijo `/n`, que permite sumarizar rutas contiguas y alineadas. → [[cm13_direccionamiento-ip|Cap. 13]]

> [!question]- 46. Protocolo enrutado vs. de enrutamiento.
> El enrutado transporta datos con direcciones (IP); el de enrutamiento intercambia rutas (RIP, OSPF, BGP). → [[cm14_enrutamiento|Cap. 14]]

> [!question]- 47. RIP: métrica, límite y transporte.
> Saltos; máximo 15 (16 = inalcanzable); UDP 520; actualiza cada 30 s. → [[cm14_enrutamiento|Cap. 14]]

> [!question]- 48. OSPF: métrica y algoritmo.
> Costo (según ancho de banda) y Dijkstra/SPF; va sobre IP protocolo 89 y usa áreas. → [[cm14_enrutamiento|Cap. 14]]

> [!question]- 49. ¿Cómo detecta bucles BGP?
> Con el atributo AS_PATH: si el router ve su propio AS en la lista, descarta la ruta. → [[cm14_enrutamiento|Cap. 14]]

> [!question]- 50. ¿Qué es longest match?
> La regla por la que gana la ruta más específica (prefijo más largo) antes de comparar métricas. → [[cm14_enrutamiento|Cap. 14]]

> [!question]- 51. Describí el three-way handshake.
> SYN (ISN del cliente) → SYN-ACK (ISN del servidor + ACK) → ACK. Sincroniza ambos extremos. → [[cm15_tcp-udp-congestion|Cap. 15]]

> [!question]- 52. ¿Qué significa `ACK = 5001`?
> Que se recibió todo hasta el byte 5000 y se espera el 5001. → [[cm15_tcp-udp-congestion|Cap. 15]]

> [!question]- 53. Control de flujo vs. congestión.
> Flujo protege al receptor (ventana anunciada); congestión protege a la red (cwnd). → [[cm15_tcp-udp-congestion|Cap. 15]]

> [!question]- 54. ¿Qué es slow start?
> El crecimiento exponencial inicial de `cwnd` (se duplica por RTT) hasta `ssthresh`. → [[cm15_tcp-udp-congestion|Cap. 15]]

> [!question]- 55. ¿Qué es AIMD?
> Aumento aditivo y disminución multiplicativa: sube 1 MSS por RTT y cae a la mitad ante pérdida detectada por ACK duplicados. → [[cm15_tcp-udp-congestion|Cap. 15]]

> [!question]- 56. ¿Cuándo usarías UDP?
> Cuando la latencia importa más que la pérdida: VoIP, streaming, DNS, juegos. → [[cm15_tcp-udp-congestion|Cap. 15]]

> [!question]- 57. ¿Qué es una VPN?
> Un túnel cifrado sobre una red no confiable, que da privacidad sin infraestructura dedicada. → [[cm16_wan-mpls-moviles|Cap. 16]]

> [!question]- 58. ¿Qué es MPLS?
> Una técnica de conmutación por etiquetas de longitud fija que permite QoS, ingeniería de tráfico y VPN de capa 3. → [[cm16_wan-mpls-moviles|Cap. 16]]

> [!question]- 59. Diferenciá LER y LSR.
> LER es el borde y pone/quita la etiqueta; LSR es del núcleo y solo conmuta por etiqueta. → [[cm16_wan-mpls-moviles|Cap. 16]]

> [!question]- 60. Handoff vs. roaming.
> Handoff es el cambio de celda dentro de la misma red; roaming es usar la red de otro operador. → [[cm16_wan-mpls-moviles|Cap. 16]]

## B.8 Preguntas de integración

> [!question]- 61. Diseñá el direccionamiento para 3 sedes con 200, 60 y 20 hosts desde `192.168.0.0/23`.
> 200 → `/24` (`192.168.0.0/24`); 60 → `/26` (`192.168.1.0/26`); 20 → `/27` (`192.168.1.64/27`), todas dentro del `/23`. De mayor a menor.

> [!question]- 62. ¿Por qué no se usa RIP en Internet?
> Por el límite de 15 saltos, la convergencia lenta, la métrica por saltos y la falta de políticas entre operadores.

> [!question]- 63. Un video se corta y se pixela. ¿Qué está fallando?
> Congestión o pérdida en la red: UDP no retransmite, así que la aplicación debe adaptar la tasa o usar buffering.

> [!question]- 64. ¿Cómo se relaciona el subnetting con el ruteo?
> Cada subred es un prefijo en la tabla de ruteo; el longest match decide cuál se aplica y la sumarización reduce el tamaño de la tabla.

#libro4 #preguntas
