---
tags: [efip, programacion, anexo, oral]
anexo: B
---

# B. Banco de preguntas de oral

> [!info] Cómo usarlo
> Tapá la respuesta, contestá en voz alta en 30–90 segundos y recién después abrí. Si no podés aplicar el concepto a un ejemplo, no está aprendido.
> Recordá la regla del EFIP: **definir → cómo funciona → operaciones → aplicar al caso → justificar**.

## Sub-eje 3.1 — Java básico

> [!question]- 1. ¿Qué es un lenguaje de programación?
> Lenguaje formal con reglas sintácticas y semánticas que permite expresar algoritmos para controlar el comportamiento de un sistema informático.

> [!question]- 2. ¿Por qué Java es portable?
> Porque compila a bytecode independiente de la CPU y cada plataforma tiene una JVM que lo ejecuta.

> [!question]- 3. JDK, JRE y JVM: diferencias.
> JDK = herramientas + JRE (compila). JRE = bibliotecas + JVM (ejecuta). JVM = ejecuta bytecode.

> [!question]- 4. ¿Qué es el bytecode?
> Representación intermedia portable que genera `javac` y almacena en archivos `.class`.

> [!question]- 5. ¿Cuál es la diferencia entre error de compilación y excepción?
> El primero impide generar el `.class`; la segunda ocurre en ejecución y puede capturarse.

> [!question]- 6. Enumerá los ocho tipos primitivos.
> `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`.

> [!question]- 7. ¿Qué significa tipado fuerte?
> Que toda variable tiene un tipo declarado y el compilador controla la compatibilidad en cada asignación.

> [!question]- 8. Variable vs. constante.
> La variable puede reasignarse; la constante se declara `final` y recibe un solo valor.

> [!question]- 9. ¿Por qué `7 / 2` da 3?
> Porque ambos operandos son `int` y la división entera trunca. Para 3.5: `(double) 7 / 2`.

> [!question]- 10. Precedencia y asociatividad.
> La precedencia define qué se evalúa primero; la asociatividad, cómo se agrupan los de igual precedencia. `=` asocia a derecha.

> [!question]- 11. ¿Qué es el cortocircuito?
> `&&` no evalúa el segundo operando si el primero es `false`; `||` no lo evalúa si es `true`.

> [!question]- 12. `while` vs. `do-while`.
> `while` puede ejecutarse cero veces; `do-while` al menos una, porque evalúa al final.

> [!question]- 13. ¿Cuándo usar `switch` y cuándo `if`?
> `switch` para opciones discretas de una misma expresión; `if` para rangos y condiciones compuestas.

> [!question]- 14. ¿Qué pasa si olvidás un `break` en un `switch`?
> Se ejecuta el `case` siguiente (fall-through) hasta encontrar un `break`.

> [!question]- 15. ¿Por qué `main` es `static`?
> Porque la JVM lo invoca sin crear un objeto de la clase.

## Sub-eje 3.2 — Paradigma OO

> [!question]- 16. Clase vs. objeto.
> La clase es la definición (atributos y métodos); el objeto es una instancia con estado propio.

> [!question]- 17. ¿Qué es un mensaje?
> La invocación de un método sobre un objeto (`objeto.metodo()`), que dispara su comportamiento.

> [!question]- 18. Los cuatro pilares.
> Abstracción (lo esencial), encapsulamiento (control de acceso), herencia (es un), polimorfismo (mismo mensaje, distinta respuesta).

> [!question]- 19. ¿Cómo identificás clases en un enunciado?
> Sustantivos con identidad y responsabilidad; verbos como métodos; se valida recorriendo los casos de uso.

> [!question]- 20. Asociación, agregación y composición.
> Asociación: conoce/usa. Agregación: todo-parte débil (la parte vive sin el todo). Composición: la parte muere con el todo.

> [!question]- 21. ¿Cómo distinguís herencia de composición?
> “Es un” → herencia. “Tiene un” → composición o agregación.

## Sub-eje 3.3 — POO en Java

> [!question]- 22. ¿Qué hace `new`?
> Reserva memoria, inicializa atributos por defecto, ejecuta el constructor y devuelve la referencia.

> [!question]- 23. Reglas de un constructor.
> Mismo nombre que la clase, sin tipo de retorno, se invoca con `new`, puede estar sobrecargado.

> [!question]- 24. ¿Qué pasa si declaro un constructor con parámetros?
> Desaparece el constructor vacío por defecto; si lo necesito, debo declararlo.

> [!question]- 25. Niveles de acceso.
> `private` (clase), sin modificador (paquete), `protected` (paquete + subclases), `public` (todos).

> [!question]- 26. ¿Para qué sirve encapsular?
> Para ocultar el estado y obligar a modificarlo por operaciones que preservan los invariantes.

> [!question]- 27. Getter y setter: ¿siempre?
> No. El setter solo existe si la modificación es una operación válida del dominio; la identidad suele ser inmutable.

> [!question]- 28. Atributo de instancia vs. `static`.
> Uno por objeto vs. uno compartido por toda la clase.

> [!question]- 29. ¿Por qué un método estático no puede usar `this`?
> Porque se ejecuta sin objeto y `this` representa al objeto actual.

> [!question]- 30. Firma de un método.
> Nombre + cantidad, tipo y orden de parámetros. El tipo de retorno no forma parte de la firma.

> [!question]- 31. Sobrecarga vs. sobrescritura.
> Sobrecarga: misma clase, distinta firma, se resuelve al compilar. Sobrescritura: subclase, misma firma, se resuelve en ejecución.

> [!question]- 32. `this` y `super`.
> `this` es el objeto actual (y llama a otro constructor de la clase); `super` es la superclase (y llama a su constructor o método).

> [!question]- 33. ¿Qué se hereda y qué no?
> Se heredan atributos y métodos accesibles; **no** los constructores ni los `private` (aunque existan).

> [!question]- 34. ¿Para qué sirve `@Override`?
> Para que el compilador verifique que realmente se está sobrescribiendo un método heredado.

> [!question]- 35. Clase abstracta: reglas.
> No se instancia, puede tener estado, constructor y métodos concretos; los abstractos deben implementarse en la subclase concreta.

> [!question]- 36. ¿Cuándo clase abstracta y cuándo interfaz?
> Abstracta si hay estado o implementación compartida; interfaz si es un contrato de capacidad que varias clases pueden cumplir.

> [!question]- 37. ¿Puede una clase implementar varias interfaces?
> Sí. Solo puede extender una clase, pero implementar múltiples interfaces.

## Sub-eje 3.4 — Complementarios

> [!question]- 38. Arreglo vs. `ArrayList`.
> Arreglo: tamaño fijo, `length`, admite primitivos. `ArrayList`: dinámico, `size()`, solo objetos con genéricos.

> [!question]- 39. ¿Qué hace `remove(1)` en un `ArrayList<Integer>`?
> Elimina el elemento en el **índice** 1, no el valor 1.

> [!question]- 40. ¿Por qué no se puede eliminar dentro de un `for-each`?
> Porque modifica la estructura mientras se itera y lanza `ConcurrentModificationException`.

> [!question]- 41. `==` vs. `equals` en `String`.
> `==` compara referencias; `equals` compara contenido.

> [!question]- 42. ¿Qué es la inmutabilidad de `String`?
> Que sus métodos no modifican el objeto: devuelven una cadena nueva.

> [!question]- 43. ¿Cuándo usar `StringBuilder`?
> Cuando hay muchas concatenaciones, especialmente dentro de un ciclo.

> [!question]- 44. ¿Qué devuelve `substring(1, 3)` de `"Hola"`?
> `"ol"`: incluye el índice 1 y excluye el 3.

> [!question]- 45. Polimorfismo: ¿qué método se ejecuta?
> El del objeto real, no el del tipo de la referencia (despacho dinámico).

> [!question]- 46. ¿Qué no es polimórfico?
> Los atributos (`field hiding`) y los métodos `static`.

> [!question]- 47. Checked vs. unchecked.
> Checked: el compilador obliga a manejarla (`IOException`). Unchecked: `RuntimeException`, no obliga.

> [!question]- 48. `throw` vs. `throws`.
> `throw` lanza una excepción; `throws` la declara en la firma.

> [!question]- 49. ¿Cuándo se ejecuta `finally`?
> Siempre, haya o no excepción, incluso si hay `return` en el `try`.

> [!question]- 50. ¿Cómo leés un archivo de texto?
> `Files.readAllLines(Path)` o `BufferedReader.readLine()` con `try-with-resources`, capturando `IOException`.

## Sub-eje 4.1 — Pilas y colas

> [!question]- 51. Pila: principio y operaciones.
> LIFO. `push`, `pop`, `peek`, `isEmpty`, `size`.

> [!question]- 52. Cola: principio y operaciones.
> FIFO. `enqueue`/`offer`, `dequeue`/`poll`, `peek`, `isEmpty`, `size`.

> [!question]- 53. Pila con vector: ¿cómo se representa el tope?
> Con un índice que empieza en −1; `push` hace `datos[++tope]`, `pop` devuelve `datos[tope--]`.

> [!question]- 54. ¿Por qué la cola circular usa módulo?
> Para reutilizar posiciones liberadas: `fin = (fin + 1) % capacidad`.

> [!question]- 55. ¿Cómo distinguís cola llena de vacía?
> Con un contador `cantidad`; `frente == fin` es ambiguo sin él.

> [!question]- 56. Aplicaciones de pila y cola.
> Pila: deshacer, paréntesis, recursión. Cola: turnos, impresión, mensajes.

## Sub-eje 4.2 — Listas enlazadas

> [!question]- 57. ¿Qué es un nodo?
> Una estructura con un dato y una referencia al siguiente (y al anterior, en la doble).

> [!question]- 58. Costo de insertar al inicio.
> O(1): se enlaza el nuevo al primero y se mueve la referencia.

> [!question]- 59. Costo de acceder por índice.
> O(n): hay que recorrer desde el primero.

> [!question]- 60. ¿Qué ventaja tiene la doble?
> Recorrer en ambos sentidos y eliminar un nodo conocido en O(1).

> [!question]- 61. ¿Cómo se recorre una circular?
> Guardando la referencia inicial y parando al volver a ella, o recorriendo exactamente `cantidad` nodos.

> [!question]- 62. ¿Qué es un iterador?
> Un objeto con `hasNext()` y `next()` que recorre sin exponer los nodos internos.

> [!question]- 63. Lista ordenada: ¿qué gana y qué pierde?
> Gana corte temprano en la búsqueda y recorrido ordenado; pierde O(n) en la inserción.

## Sub-eje 4.3 — Ordenación

> [!question]- 64. Inserción: idea y complejidad.
> Inserta cada elemento en la parte ordenada; O(n) mejor, O(n²) promedio y peor, estable, in-place.

> [!question]- 65. Shellsort: idea.
> Inserciones con gaps decrecientes hasta 1; in-place, no estable, costo según la secuencia de gaps.

> [!question]- 66. Mergesort: idea y complejidad.
> Divide en mitades y mezcla; O(n log n) siempre, O(n) de memoria, estable.

> [!question]- 67. Quicksort: idea y complejidad.
> Elige pivote y particiona; promedio O(n log n), peor O(n²), in-place, no estable.

> [!question]- 68. ¿Cuándo Quicksort es O(n²)?
> Con pivotes que siempre dejan un lado vacío, por ejemplo arreglo ordenado con pivote en un extremo.

> [!question]- 69. ¿Qué significa estable?
> Que elementos con igual clave conservan su orden relativo.

> [!question]- 70. ¿Qué algoritmo elegir con pocos datos casi ordenados?
> Inserción: mejor caso O(n), simple y estable.

> [!question]- 71. ¿Qué algoritmo elegir si necesito garantía de peor caso?
> Mergesort: O(n log n) garantizado, a costa de O(n) de memoria.

> [!question]- 72. ¿Por qué Mergesort necesita memoria auxiliar?
> Porque la mezcla requiere comparar y escribir en un arreglo temporal sin pisar elementos aún no leídos.

## Preguntas integradoras

> [!question]- 73. ¿Cómo modelás un sistema de semáforos y cámaras?
> `Dispositivo` abstracta con `id` y `tipo()`, `Semaforo` y `Camara` como subclases, `Activable` como interfaz, `ArrayList` para la colección, cola para alertas y pila para deshacer.

> [!question]- 74. ¿Qué estructura usarías para las alertas y por qué?
> Una cola, porque deben atenderse por orden de llegada (FIFO) y no se debe saltear ninguna.

> [!question]- 75. ¿Qué estructura para deshacer acciones?
> Una pila, porque la última acción debe revertirse primero (LIFO).

> [!question]- 76. ¿Cómo justificás una elección de estructura?
> Definiendo la regla de acceso (LIFO/FIFO/índice), el costo de las operaciones dominantes y el requisito del dominio.

#libro1 #anexo #oral
