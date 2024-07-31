## Bucles

Los bucles permiten ejecutar un bloque de código repetidamente mientras se cumpla una condición específica. En Java, hay cuatro tipos principales de bucles: `for`, `while`, `do-while`, y `for-each`.

### 1. `for`

El bucle `for` se usa cuando se conoce de antemano el número de iteraciones. Consiste en una inicialización, una condición y un incremento o decremento.

**Sintaxis básica:**
```java
for (inicialización; condición; incremento/decremento) {
    // Bloque de código a ejecutar
}
```
**Ejemplo:**
```java
for (int i = 0; i < 10; i++) {
    System.out.println(i); // Imprime los números del 0 al 9
}
```

### 2. `while`

El bucle `while` se ejecuta mientras la condición especificada sea `true`. Se usa cuando no se conoce de antemano el número de iteraciones.

**Sintaxis básica:**
```java
while (condición) {
    // Bloque de código a ejecutar
}
```
**Ejemplo:**
```java
int i = 0;
while (i < 10) {
    System.out.println(i); // Imprime los números del 0 al 9
    i++;
}
```
### 3. `do-while`

El bucle `do-while` es similar al bucle `while`, pero garantiza que el bloque de código se ejecute al menos una vez antes de verificar la condición.

**Sintaxis básica:**
```java
do {
    // Bloque de código a ejecutar
} while (condición);
```
**Ejemplo:**
```java
int i = 0;
do {
    System.out.println(i); // Imprime los números del 0 al 9
    i++;
} while (i < 10);
```
### 4. `for-each`

El bucle `for-each` se usa para iterar sobre elementos de una colección o arreglo. Es útil para recorrer arreglos y colecciones como listas y conjuntos.

**Sintaxis básica:**
```java
for (tipo elemento : colección) {
    // Bloque de código a ejecutar
}
```
**Ejemplo:**
```java
int[] numeros = {1, 2, 3, 4, 5};
for (int numero : numeros) {
    System.out.println(numero); // Imprime los números del 1 al 5
}
```
### Ejemplos Completos

Aquí tienes ejemplos completos de cada tipo de bucle en Java:

**Bucle `for`:**

```java
public class EjemploFor {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            System.out.println(i);
        }
    }
}
```

**Bucle `while`:**

```java
public class EjemploWhile {
    public static void main(String[] args) {
        int i = 0;
        while (i < 10) {
            System.out.println(i);
            i++;
        }
    }
}
```

**Bucle `do-while`:**

```java
public class EjemploDoWhile {
    public static void main(String[] args) {
        int i = 0;
        do {
            System.out.println(i);
            i++;
        } while (i < 10);
    }
}
```

**Bucle `for-each`:**

```java
public class EjemploForEach {
    public static void main(String[] args) {
        int[] numeros = {1, 2, 3, 4, 5};
        for (int numero : numeros) {
            System.out.println(numero);
        }
    }
}
```

### Conclusión

Los bucles son fundamentales en la programación para ejecutar bloques de código repetidamente bajo condiciones específicas. Java proporciona diversas estructuras de bucles para diferentes necesidades, desde iteraciones conocidas hasta recorridos de colecciones.

### Consideraciones Adicionales

- **Condiciones Infinitas:** Asegúrate de que los bucles `while` y `do-while` tengan condiciones que eventualmente se vuelvan `false` para evitar bucles infinitos.
- **Eficiencia:** Usa el bucle adecuado según el contexto para mejorar la legibilidad y eficiencia del código.
- **Colecciones:** El bucle `for-each` es ideal para iterar sobre colecciones y arreglos, proporcionando una sintaxis más limpia y concisa.
- **Interrupciones y Continuaciones:** Conoce el uso de las declaraciones `break` y `continue` para controlar el flujo dentro de los bucles.