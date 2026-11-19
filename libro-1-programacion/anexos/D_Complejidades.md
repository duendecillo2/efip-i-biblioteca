---
tags: [efip, programacion, anexo, complejidad]
anexo: D
---

# D. Complejidades y mapa del programa

> [!info] Cómo usarlo
> Dos usos: la tabla de complejidades para 4.3 y el mapa de lecturas oficiales para verificar cobertura. No memorices la tabla sin entender **qué operación** mide cada fila.

## D.1 Estructuras de datos

| Estructura | Acceso por índice | Búsqueda | Inserción al inicio | Inserción al final | Eliminación al inicio | Memoria |
|---|---|---|---|---|---|---|
| Arreglo | O(1) | O(n) | O(n) | O(n) | O(n) | O(n) |
| `ArrayList` | O(1) | O(n) | O(n) | O(1) amortizado | O(n) | O(n) |
| Lista simple | O(n) | O(n) | O(1) | O(n)* | O(1) | O(n) |
| Lista doble | O(n) | O(n) | O(1) | O(1) | O(1) | O(n) |
| Pila | — | — | — | `push` O(1) | — | O(n) |
| Cola | — | — | — | `enqueue` O(1) | `dequeue` O(1) | O(n) |

\* O(1) si se mantiene una referencia al último nodo.

> [!important] Cómo leerla
> “La lista es más rápida” no significa nada. Hay que decir **para qué operación**. Insertar al inicio: lista O(1) vs. arreglo O(n). Acceder por índice: arreglo O(1) vs. lista O(n).

## D.2 Operaciones sobre listas

| Operación | Lista simple | Lista doble | Lista circular | Lista ordenada |
|---|---|---|---|---|
| Insertar al inicio | O(1) | O(1) | O(1) | O(n) |
| Insertar al final | O(n) | O(1) | O(1) | O(n) |
| Buscar | O(n) | O(n) | O(n) | O(n), con corte |
| Eliminar conocido | O(n) | **O(1)** | O(n) | O(n) |
| Recorrer | O(n) | O(n) | O(n) | O(n) |

## D.3 Ordenación

| Algoritmo | Mejor | Promedio | Peor | Memoria | Estable | In-place |
|---|---|---|---|---|---|---|
| Inserción | O(n) | O(n²) | O(n²) | O(1) | Sí | Sí |
| Shellsort | Depende | Depende | O(n²) | O(1) | No | Sí |
| Mergesort | O(n log n) | O(n log n) | **O(n log n)** | **O(n)** | **Sí** | No |
| Quicksort | O(n log n) | O(n log n) | **O(n²)** | O(log n) | No | Sí |

### Cómo se lee cada columna

| Columna | Significado |
|---|---|
| Mejor | Con datos ya ordenados o condiciones ideales |
| Promedio | Con datos aleatorios |
| Peor | Con datos adversos (ordenados al revés, pivotes malos) |
| Memoria | Espacio adicional además del arreglo |
| Estable | Conserva el orden relativo de claves iguales |
| In-place | No necesita otra estructura del tamaño de n |

## D.4 Búsqueda

| Algoritmo | Requisito | Costo |
|---|---|---|
| Lineal | Ninguno | O(n) |
| Binaria | Datos **ordenados** | O(log n) |

> [!warning] La búsqueda binaria no está en el programa
> Se menciona solo para comparar. Si la usás en un ejercicio, aclaralo y no la presentes como obligatoria.

## D.5 Crecimiento

| n | log n | n log n | n² |
|---:|---:|---:|---:|
| 10 | 3,3 | 33 | 100 |
| 100 | 6,6 | 664 | 10.000 |
| 1.000 | 10 | 10.000 | 1.000.000 |
| 10.000 | 13 | 133.000 | 100.000.000 |

> [!important] Lo que hay que poder decir
> “Para n = 10.000, un algoritmo O(n²) hace cien millones de operaciones; uno O(n log n), alrededor de ciento treinta mil. Por eso la diferencia se nota a partir de conjuntos medianos.”

## D.6 Reglas para justificar

1. Nombrá la **operación** (no “la estructura”).
2. Distinguí **mejor / promedio / peor**.
3. Aclarí **memoria** y **estabilidad** si el problema lo pide.
4. Cerrá con la **decisión**: “elijo X porque el caso tiene Y”.

Ejemplo de respuesta completa:

> “Para 20 elementos casi ordenados elijo **inserción**: su mejor caso es O(n), es estable e in-place. No necesito la garantía de Mergesort y evito su O(n) de memoria auxiliar.”

#libro1 #anexo #complejidad


## D.7 Cobertura del canon

Base: POO — INF382, 16 lecturas (`poo-y-taller-alg-1`), ya condensadas en 20 capítulos.

| Lectura | Título oficial | Capítulo(s) |
|---|---|---|
| M0L1 | Algoritmos y pensamiento lógico | [[01_paradigmas-y-jvm\|1]] · [[03_control-y-estructura\|3]] |
| M0L2 | Paradigmas de programación | [[01_paradigmas-y-jvm\|1]] |
| M0L3 | Conceptos fundamentales de la POO | [[04_paradigma-oo-y-uml\|4]] · [[05_clase-y-objeto\|5]] |
| M0L4 | Lenguajes y nociones de Java | [[01_paradigmas-y-jvm\|1]] |
| M1L1 | Lenguajes de programación | [[01_paradigmas-y-jvm\|1]] |
| M1L2 | ¿Qué es Java? | [[01_paradigmas-y-jvm\|1]] |
| M1L3 | Sintaxis | [[03_control-y-estructura\|3]] |
| M1L4 | Variables y constantes | [[02_tipos-y-operadores\|2]] |
| M2L1 | Dos paradigmas | [[01_paradigmas-y-jvm\|1]] · [[04_paradigma-oo-y-uml\|4]] |
| M2L2 | Pilas | [[16_pilas-y-colas\|16]] |
| M2L3 | Abstracción y polimorfismo | [[11_polimorfismo-y-static\|11]] |
| M2L4 | Ventajas de la POO | [[04_paradigma-oo-y-uml\|4]] |
| M3L1 | Polimorfismo en Java | [[11_polimorfismo-y-static\|11]] |
| M3L2 | Encapsulamiento | [[07_encapsulamiento\|7]] |
| M3L3 | Clases abstractas | [[09_clases-abstractas\|9]] |
| M3L4 | Ejemplos de POO | [[08_herencia\|8]] · [[10_interfaces\|10]] |
| M4L1 | Arreglos | [[12_arreglos-y-arraylist\|12]] |
| M4L2 | Strings | [[13_string\|13]] |
| M4L3 | Excepciones | [[14_excepciones\|14]] |
| M4L4 | Archivos | [[15_archivos\|15]] |

## D.8 Cobertura por sub-eje

| Sub-eje | Capítulos | Estado |
|---|---|---|
| **3.1** Java: lenguajes, sintaxis, tipos, operadores, control | 1 · 2 · 3 | ✅ |
| **3.2** Paradigma OO: conceptos, objeto, clase, atributos, métodos | 4 · 5 · 11 | ✅ |
| **3.3** POO en Java: constructores, acceso, `main`, `static`, sobrecarga, `this`/`super`, abstracta, interface | 6 · 7 · 8 · 9 · 10 · 11 | ✅ |
| **3.4** Arreglos, `ArrayList`, `String`, polimorfismo, comparación, excepciones, archivos | 11 · 12 · 13 · 14 · 15 | ✅ |
| **4.1** Pilas y colas | 16 | ✅ |
| **4.2** Listas enlazadas, dobles, circulares y ordenadas | 17 · 18 | ✅ |
| **4.3** Inserción, Shellsort, Mergesort, Quicksort | 19 · 20 | ✅ |

## D.9 Fuentes

| Bloque | Canon Siglo 21 | Complemento |
|---|---|---|
| 1–3 | Módulos 0 y 1 | UP Lab I; UNLP Programación 1 |
| 4–11 | Módulos 2 y 3 | UNLP OO1; UP Lab I 04–05; Larman (GRASP) |
| 12–15 | Módulo 4 | UP Lab I 06–08; UNLP colecciones |
| 16–20 | INF386 (no incluido en la carpeta canon) | Weiss, Sznajdleder, UNLP AYED, UP EDA |

> [!important] Hueco declarado
> La carpeta canon trae las 16 lecturas de **POO**. Las estructuras del Taller (16–20) se apoyan en la bibliografía de la cátedra y en UNLP/UP, y se declaran como Parte 4.

## D.10 Fuera del programa

| Tema | Motivo |
|---|---|
| Árboles, grafos, hashing | Fuera del EFIP |
| Hilos, sockets, GUI | Fuera del alcance |
| Patrones GoF | Libro 3, anexo opcional |

#libro1 #anexo #complejidad #mapa
