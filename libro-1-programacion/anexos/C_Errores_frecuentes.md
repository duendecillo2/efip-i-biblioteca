---
tags: [efip, programacion, anexo, errores]
anexo: C
---

# C. Errores frecuentes

> [!info] Cómo usarlo
> Antes de un simulacro, leé solo esta lista. Después del simulacro, marcá los que cometiste. Es el registro de errores en formato tabla.

## C.1 Compilación

| Error | Mensaje típico | Causa | Solución |
|---|---|---|---|
| Falta `;` | `';' expected` | Sentencia sin cerrar | Agregar `;` |
| Llave sin cerrar | `reached end of file while parsing` | `{` o `}` desbalanceada | Contar llaves |
| Nombre de archivo | `class X is public, should be declared in a file named X.java` | Clase pública y archivo distintos | Renombrar el archivo |
| Símbolo no encontrado | `cannot find symbol` | `import` faltante o tipeo | Revisar nombre e import |
| Variable no inicializada | `variable x might not have been initialized` | Local sin valor | Inicializar |
| Tipo incompatible | `incompatible types` | Asignar `double` a `int` sin cast | Cast explícito |
| Retorno faltante | `missing return statement` | Método con retorno sin `return` | Agregar `return` en todos los caminos |
| `main` mal declarado | `Main method not found` | Falta `static` o firma distinta | `public static void main(String[] args)` |
| Método no estático desde estático | `non-static method cannot be referenced` | Llamar método de instancia desde `main` | Crear objeto o hacer el método `static` |
| `this` en estático | `non-static variable this cannot be referenced` | Contexto sin objeto | Quitar `this` o hacer el método de instancia |

## C.2 Ejecución

| Excepción | Cuándo | Prevención |
|---|---|---|
| `NullPointerException` | Usar una referencia `null` | Verificar antes de invocar |
| `ArrayIndexOutOfBoundsException` | Índice ≥ `length` o negativo | `i < length` |
| `StringIndexOutOfBoundsException` | `charAt`/`substring` fuera de rango | Validar longitud |
| `ArithmeticException: / by zero` | División entera por 0 | Validar divisor |
| `NumberFormatException` | `parseInt` con texto no numérico | `try/catch` |
| `ClassCastException` | Downcast a tipo incorrecto | `instanceof` antes |
| `IndexOutOfBoundsException` | `get`/`remove` con índice inválido en lista | Validar `0 <= i < size()` |
| `ConcurrentModificationException` | Modificar colección mientras se itera | Recorrer al revés o `removeIf` |
| `StackOverflowError` | Recursión sin caso base | Definir caso base |
| `IllegalStateException` | Operación inválida para el estado (pila vacía) | Validar estado |
| `NoSuchElementException` | `Scanner` o iterador sin elementos | `hasNext()` |
| `IOException` no capturada | Operación de archivo sin `try/catch` | `try-with-resources` + catch |

## C.3 Errores conceptuales

| Error | Corrección |
|---|---|
| “Pila = FIFO, cola = LIFO” | **Pila = LIFO**, **cola = FIFO** |
| “Java es interpretado” | Compila a bytecode; la JVM lo ejecuta (híbrido) |
| “El JRE compila” | Compila el **JDK** |
| “`String` es un tipo primitivo” | Es una **clase** |
| “`==` compara contenido de `String`” | Compara **referencias**; contenido con `equals` |
| “El retorno distingue sobrecargas” | Solo la firma (nombre + parámetros) |
| “Los constructores se heredan” | No se heredan; se invocan con `super(...)` |
| “Los `private` se heredan” | Existen, pero no son accesibles |
| “Una clase abstracta se instancia con `new`” | No se instancia |
| “Una interfaz se extiende con `extends` desde una clase” | Se implementa con `implements` |
| “`static` es polimórfico” | No: se resuelve por el tipo de la referencia |
| “Los atributos son polimórficos” | No: se ocultan, no se sobrescriben |
| “`ArrayList` guarda primitivos” | Guarda objetos (`Integer`, `Double`…) |
| “`remove(1)` elimina el valor 1” | Elimina el **índice** 1 |
| “Mergesort es in-place” | Usa O(n) de memoria |
| “Quicksort es estable” | No es estable |
| “Shellsort siempre es O(n log n)” | Depende de los gaps; peor O(n²) |
| “Todo `catch` debe ir en cualquier orden” | Del más específico al más general |
| “`finally` no se ejecuta con `return`” | Se ejecuta siempre |
| “La lista enlazada accede por índice en O(1)” | Es O(n) |

## C.4 Errores de diseño (los que bajan nota en el oral)

| Error | Por qué está mal | Cómo corregirlo |
|---|---|---|
| Herencia sin “es un” | Acopla innecesariamente | Composición |
| Atributos públicos | Rompen el encapsulamiento | `private` + métodos |
| Setter para todo | El estado queda sin protección | Solo operaciones del dominio |
| Clase “Gestor” que hace todo | Baja cohesión | Repartir responsabilidades |
| `instanceof` en cadena | El polimorfismo no se está usando | Método en la clase padre |
| Duplicar código en subclases | Mantenimiento costoso | Subir a la clase base |
| `catch` vacío | Oculta errores | Registrar o relanzar |
| Nombres `a`, `b`, `x1` | Ilegibilidad | Nombres del dominio |
| Comentar lo obvio | Ruido | Comentar decisiones |

## C.5 Checklist de 60 segundos antes de entregar

- [ ] El archivo se llama igual que la clase pública.
- [ ] Todos los `;` y llaves están.
- [ ] No usé `=` donde iba `==`.
- [ ] Los ciclos tienen condición de corte que se cumple.
- [ ] Los índices van de `0` a `length - 1` / `size() - 1`.
- [ ] Inicialicé las variables locales.
- [ ] No llamé métodos de instancia desde `main` sin objeto.
- [ ] Cerré los archivos o usé `try-with-resources`.
- [ ] Los `catch` van del más específico al más general.
- [ ] Los nombres siguen las convenciones.

#libro1 #anexo #errores
