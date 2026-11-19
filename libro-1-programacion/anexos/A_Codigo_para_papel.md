---
tags: [efip, programacion, anexo, codigo]
anexo: A
---

# A. Código listo para papel

> [!info] Para qué sirve
> Los fragmentos que más se piden escribir a mano. Están completos, compilan y son cortos a propósito. Practicá escribirlos **sin mirar**.

## A.1 Clase con encapsulamiento y validación

```java
public class Cuenta {

    private final String titular;
    private double saldo;

    public Cuenta(String titular, double saldoInicial) {
        if (titular == null || titular.isBlank()) {
            throw new IllegalArgumentException("Titular obligatorio");
        }
        if (saldoInicial < 0) {
            throw new IllegalArgumentException("Saldo inválido");
        }
        this.titular = titular;
        this.saldo = saldoInicial;
    }

    public void depositar(double monto) {
        if (monto <= 0) throw new IllegalArgumentException("Monto inválido");
        saldo += monto;
    }

    public void extraer(double monto) {
        if (monto <= 0) throw new IllegalArgumentException("Monto inválido");
        if (monto > saldo) throw new IllegalStateException("Saldo insuficiente");
        saldo -= monto;
    }

    public double getSaldo() { return saldo; }
    public String getTitular() { return titular; }
}
```

## A.2 Herencia + abstracta + interface

```java
interface Activable {
    void activar();
    void desactivar();
    boolean estaActivo();
}

abstract class Dispositivo implements Activable {

    protected final String id;
    protected boolean activo;

    protected Dispositivo(String id) {
        this.id = id;
    }

    @Override public void activar()    { activo = true; }
    @Override public void desactivar() { activo = false; }
    @Override public boolean estaActivo() { return activo; }

    public abstract String tipo();

    public String ficha() {
        return tipo() + " " + id + (activo ? " [ON]" : " [OFF]");
    }
}

class Semaforo extends Dispositivo {
    private String color = "ROJO";

    Semaforo(String id) { super(id); }

    @Override public String tipo() { return "Semaforo"; }

    public void cambiarColor(String c) { color = c; }

    @Override public String ficha() { return super.ficha() + " " + color; }
}
```

## A.3 Polimorfismo en un recorrido

```java
Dispositivo[] red = {
    new Semaforo("S-01"),
    new Camara("C-01")
};

for (Dispositivo d : red) {
    d.activar();
    System.out.println(d.ficha());
}
```

## A.4 Arreglos: recorrido, máximo, promedio

```java
int[] v = {4, 9, 2, 7};

int max = v[0];
int suma = 0;

for (int x : v) {
    if (x > max) max = x;
    suma += x;
}

double promedio = (double) suma / v.length;
```

## A.5 ArrayList: alta, baja y recorrido

```java
import java.util.ArrayList;

ArrayList<String> lista = new ArrayList<>();

lista.add("A");
lista.add("B");
lista.set(0, "Z");

// eliminar al revés para no saltear
for (int i = lista.size() - 1; i >= 0; i--) {
    if (lista.get(i).equals("B")) lista.remove(i);
}

for (String s : lista) System.out.println(s);
```

## A.6 Pila con vector

```java
public class PilaArray {

    private final int[] datos;
    private int tope = -1;

    public PilaArray(int capacidad) { datos = new int[capacidad]; }

    public void push(int x) {
        if (tope == datos.length - 1) throw new IllegalStateException("Llena");
        datos[++tope] = x;
    }

    public int pop() {
        if (tope == -1) throw new IllegalStateException("Vacía");
        return datos[tope--];
    }

    public int peek() {
        if (tope == -1) throw new IllegalStateException("Vacía");
        return datos[tope];
    }

    public boolean isEmpty() { return tope == -1; }
    public int size() { return tope + 1; }
}
```

## A.7 Pila con lista

```java
public class PilaLista {

    private static class Nodo {
        int dato;
        Nodo siguiente;
        Nodo(int dato, Nodo siguiente) {
            this.dato = dato;
            this.siguiente = siguiente;
        }
    }

    private Nodo cima;

    public void push(int x) { cima = new Nodo(x, cima); }

    public int pop() {
        if (cima == null) throw new IllegalStateException("Vacía");
        int v = cima.dato;
        cima = cima.siguiente;
        return v;
    }

    public int peek() {
        if (cima == null) throw new IllegalStateException("Vacía");
        return cima.dato;
    }

    public boolean isEmpty() { return cima == null; }
}
```

## A.8 Cola circular

```java
public class ColaCircular {

    private final int[] datos;
    private int frente, fin, cantidad;

    public ColaCircular(int capacidad) { datos = new int[capacidad]; }

    public void enqueue(int x) {
        if (cantidad == datos.length) throw new IllegalStateException("Llena");
        datos[fin] = x;
        fin = (fin + 1) % datos.length;
        cantidad++;
    }

    public int dequeue() {
        if (cantidad == 0) throw new IllegalStateException("Vacía");
        int v = datos[frente];
        frente = (frente + 1) % datos.length;
        cantidad--;
        return v;
    }

    public boolean isEmpty() { return cantidad == 0; }
    public int size() { return cantidad; }
}
```

## A.9 Cola con lista

```java
public class ColaLista {

    private static class Nodo {
        int dato;
        Nodo siguiente;
        Nodo(int dato) { this.dato = dato; }
    }

    private Nodo frente, fin;

    public void enqueue(int x) {
        Nodo n = new Nodo(x);
        if (frente == null) frente = n;
        else fin.siguiente = n;
        fin = n;
    }

    public int dequeue() {
        if (frente == null) throw new IllegalStateException("Vacía");
        int v = frente.dato;
        frente = frente.siguiente;
        if (frente == null) fin = null;
        return v;
    }

    public boolean isEmpty() { return frente == null; }
}
```

## A.10 Lista simple: insertar, eliminar, recorrer

```java
public class ListaSimple {

    private static class Nodo {
        int dato;
        Nodo siguiente;
        Nodo(int dato) { this.dato = dato; }
    }

    private Nodo primero;
    private int cantidad;

    public void agregarAlInicio(int x) {
        Nodo n = new Nodo(x);
        n.siguiente = primero;      // enlazar primero
        primero = n;                // mover después
        cantidad++;
    }

    public boolean eliminar(int x) {
        if (primero == null) return false;

        if (primero.dato == x) {
            primero = primero.siguiente;
            cantidad--;
            return true;
        }

        Nodo ant = primero;
        Nodo act = primero.siguiente;

        while (act != null) {
            if (act.dato == x) {
                ant.siguiente = act.siguiente;
                cantidad--;
                return true;
            }
            ant = act;
            act = act.siguiente;
        }
        return false;
    }

    public void mostrar() {
        Nodo a = primero;
        while (a != null) {
            System.out.print(a.dato + " ");
            a = a.siguiente;
        }
        System.out.println();
    }
}
```

## A.11 Inserción y Shellsort

```java
static void insercion(int[] v) {
    for (int i = 1; i < v.length; i++) {
        int actual = v[i];
        int j = i - 1;
        while (j >= 0 && v[j] > actual) {
            v[j + 1] = v[j];
            j--;
        }
        v[j + 1] = actual;
    }
}

static void shell(int[] v) {
    for (int gap = v.length / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < v.length; i++) {
            int actual = v[i];
            int j = i;
            while (j >= gap && v[j - gap] > actual) {
                v[j] = v[j - gap];
                j -= gap;
            }
            v[j] = actual;
        }
    }
}
```

## A.12 Mergesort

```java
static void mergeSort(int[] v, int izq, int der) {
    if (izq >= der) return;

    int medio = (izq + der) / 2;
    mergeSort(v, izq, medio);
    mergeSort(v, medio + 1, der);

    int[] aux = new int[der - izq + 1];
    int i = izq, j = medio + 1, k = 0;

    while (i <= medio && j <= der) {
        aux[k++] = (v[i] <= v[j]) ? v[i++] : v[j++];
    }
    while (i <= medio) aux[k++] = v[i++];
    while (j <= der) aux[k++] = v[j++];

    for (int x = 0; x < aux.length; x++) v[izq + x] = aux[x];
}
```

## A.13 Quicksort

```java
static void quickSort(int[] v, int izq, int der) {
    if (izq >= der) return;

    int pivote = v[der];
    int i = izq - 1;

    for (int j = izq; j < der; j++) {
        if (v[j] <= pivote) {
            i++;
            int aux = v[i]; v[i] = v[j]; v[j] = aux;
        }
    }

    int aux = v[i + 1]; v[i + 1] = v[der]; v[der] = aux;

    quickSort(v, izq, i);
    quickSort(v, i + 2, der);
}
```

> [!warning] Verificá los índices
> Al copiar de memoria, revisá que la recursión use `i` y `i + 2`. Un error de índice acá produce `StackOverflowError` o un arreglo mal ordenado.

## A.14 Leer un archivo

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.io.IOException;

try {
    for (String linea : Files.readAllLines(Path.of("datos.txt"))) {
        System.out.println(linea);
    }
} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
}
```

## A.15 Escribir un archivo

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

Files.write(Path.of("salida.txt"), List.of("linea 1", "linea 2"));
```

#libro1 #anexo #codigo
