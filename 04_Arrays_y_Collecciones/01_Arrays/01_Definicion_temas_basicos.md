### Manipulación de Arreglos en Java

Los arreglos en Java son estructuras de datos que permiten almacenar múltiples valores del mismo tipo. Entender cómo crear y manipular arreglos es fundamental para la certificación de Java.

### 1. Crear Arreglos

Para declarar un arreglo en Java, se especifica el tipo de los elementos seguido de corchetes `[]`. La creación del arreglo puede realizarse de varias maneras.

*Declaración y Creación de un Arreglo*:
```java
int[] numeros = new int[5];
String[] nombres = {"Alice", "Bob", "Charlie"};
```

*Inicialización*:
```java
int[] numeros = {1, 2, 3, 4, 5};
```

### 2. Agregar Elementos

En los arreglos de Java, el tamaño es fijo una vez creado. No se pueden agregar elementos directamente. Se necesita crear un nuevo arreglo más grande y copiar los elementos del arreglo original.

*Ejemplo de agregar elementos a un arreglo*:
```java
int[] original = {1, 2, 3};
int[] nuevo = new int[original.length + 1];
System.arraycopy(original, 0, nuevo, 0, original.length);
nuevo[nuevo.length - 1] = 4;
```

### 3. Eliminar Elementos

Para eliminar un elemento de un arreglo, se debe crear un nuevo arreglo más pequeño y copiar los elementos deseados.

*Ejemplo de eliminar elementos de un arreglo*:
```java
int[] original = {1, 2, 3, 4};
int[] nuevo = new int[original.length - 1];
int index = 2; // Índice del elemento a eliminar
for (int i = 0, k = 0; i < original.length; i++) {
    if (i == index) {
        continue;
    }
    nuevo[k++] = original[i];
}
```

### 4. Actualizar Elementos

Actualizar un elemento en un arreglo es directo, ya que se puede acceder a los elementos por su índice.

*Ejemplo de actualización de elementos*:
```java
int[] numeros = {1, 2, 3};
numeros[1] = 10; // Cambia el valor en el índice 1 a 10
```

### 5. Recuperar Elementos

Para recuperar un elemento, se accede al índice deseado.

*Ejemplo de recuperación de elementos*:
```java
int[] numeros = {1, 2, 3};
int numero = numeros[2]; // Recupera el valor en el índice 2
```

### 6. Ordenar Arreglos

Java proporciona métodos para ordenar arreglos en la clase `Arrays`.

*Ejemplo de ordenación de arreglos*:
```java
import java.util.Arrays;

int[] numeros = {3, 1, 4, 1, 5, 9};
Arrays.sort(numeros); // Ordena el arreglo en orden ascendente
```

### Conclusión y Consideraciones Adicionales

La manipulación de arreglos en Java implica entender cómo manejar su tamaño fijo. Las operaciones de agregar y eliminar elementos requieren crear nuevos arreglos y copiar datos, lo que puede ser ineficiente para grandes volúmenes de datos. En estos casos, puede ser más adecuado utilizar colecciones como `ArrayList` que permiten una manipulación más flexible y eficiente.

---

### Ejemplo Completo

A continuación, se muestra un ejemplo completo que incluye la creación, actualización, eliminación y ordenación de un arreglo:

```java
import java.util.Arrays;

public class ManejoArreglos {
    public static void main(String[] args) {
        // Crear arreglo
        int[] numeros = {5, 3, 8, 2, 9};
        
        // Actualizar elemento
        numeros[2] = 10; // Cambia 8 por 10
        
        // Eliminar elemento
        int indexEliminar = 1; // Índice del elemento a eliminar
        int[] nuevoArreglo = new int[numeros.length - 1];
        for (int i = 0, k = 0; i < numeros.length; i++) {
            if (i != indexEliminar) {
                nuevoArreglo[k++] = numeros[i];
            }
        }
        numeros = nuevoArreglo;
        
        // Ordenar arreglo
        Arrays.sort(numeros);
        
        // Recuperar y mostrar elementos
        for (int numero : numeros) {
            System.out.println(numero);
        }
    }
}
```
