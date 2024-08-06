### Uso de Streams de Objetos y Primitivos en Java

Java Streams proporciona una API poderosa y flexible para procesar secuencias de datos de manera funcional. Los Streams se pueden utilizar para realizar operaciones como suministrar, filtrar, mapear, consumir y ordenar datos.

#### Stream de Objetos

Los Streams de objetos procesan secuencias de objetos y proporcionan una variedad de métodos para manipular estos datos de manera funcional.

**Operaciones Básicas con Streams**

**1. Creación de Streams**

Puedes crear Streams a partir de colecciones, arrays, o mediante métodos de fábrica de la clase `Stream`.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Stream;

public class StreamCreationExample {
    public static void main(String[] args) {
        // Desde una colección
        List<String> lista = Arrays.asList("Manzana", "Banana", "Cereza");
        Stream<String> streamDesdeLista = lista.stream();
        
        // Desde un array
        String[] array = {"Manzana", "Banana", "Cereza"};
        Stream<String> streamDesdeArray = Arrays.stream(array);
        
        // Desde un método de fábrica
        Stream<String> streamDirecto = Stream.of("Manzana", "Banana", "Cereza");
    }
}
```

**2. Filtrado (filter)**

El método `filter` se utiliza para excluir elementos que no cumplen con un criterio especificado.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamFilterExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Mango");
        
        List<String> filtradas = frutas.stream()
                                       .filter(f -> f.startsWith("M"))
                                       .collect(Collectors.toList());
        
        filtradas.forEach(System.out::println); // Imprime "Mango"
    }
}
```

**3. Mapeo (map)**

El método `map` se utiliza para transformar los elementos de un Stream en otros objetos.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamMapExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");
        
        List<Integer> longitudes = frutas.stream()
                                         .map(String::length)
                                         .collect(Collectors.toList());
        
        longitudes.forEach(System.out::println); // Imprime las longitudes de las frutas
    }
}
```

#### Consumo (forEach)

El método `forEach` se utiliza para realizar una acción sobre cada elemento del Stream. Es una operación terminal que itera sobre cada elemento del Stream y aplica una función a cada uno de ellos.

**Ejemplo de Consumo con forEach:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamForEachExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");
        
        frutas.stream().forEach(System.out::println); // Imprime cada fruta
    }
}
```

En este ejemplo, la función `System.out::println` se aplica a cada elemento del Stream, imprimiendo cada fruta en la consola. El método `forEach` es útil para realizar operaciones de consumo como impresión, acumulación en estructuras de datos o cualquier otra acción que necesite aplicarse a cada elemento.

#### Ordenamiento (sorted)

El método `sorted` se utiliza para ordenar los elementos de un Stream. Puede aceptar un comparador para definir un orden personalizado o utilizar el orden natural de los elementos si son comparables.

**Ejemplo de Ordenamiento con sorted:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamSortedExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Mango");
        
        List<String> ordenadas = frutas.stream()
                                       .sorted()
                                       .collect(Collectors.toList());
        
        ordenadas.forEach(System.out::println); // Imprime las frutas ordenadas
    }
}
```

En este ejemplo, las frutas se ordenan en orden alfabético natural. El método `sorted` sin argumentos utiliza el orden natural de los elementos, pero también puede aceptar un comparador personalizado.

**Ejemplo de Ordenamiento con Comparador Personalizado:**

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

public class StreamCustomSortedExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Mango");
        
        List<String> ordenadasPorLongitud = frutas.stream()
                                                  .sorted(Comparator.comparingInt(String::length))
                                                  .collect(Collectors.toList());
        
        ordenadasPorLongitud.forEach(System.out::println); // Imprime las frutas ordenadas por longitud
    }
}
```

En este ejemplo, las frutas se ordenan por la longitud de sus nombres. El comparador `Comparator.comparingInt(String::length)` se utiliza para definir el orden de los elementos.

#### Streams Primitivos

Java proporciona Streams específicos para tipos primitivos (`IntStream`, `LongStream`, `DoubleStream`), optimizados para el procesamiento de datos primitivos.

**Ejemplo de IntStream:**

```java
import java.util.stream.IntStream;

public class IntStreamExample {
    public static void main(String[] args) {
        // Creación de un IntStream
        IntStream intStream = IntStream.range(1, 10); // 1 a 9
        
        // Sumar los elementos del Stream
        int suma = intStream.sum();
        
        System.out.println("Suma: " + suma); // Imprime la suma de 1 a 9
    }
}
```

**Operaciones en Streams Primitivos:**

- **Suministro:** `IntStream.of(1, 2, 3)`
- **Filtrado:** `intStream.filter(n -> n % 2 == 0)`
- **Mapeo:** `intStream.map(n -> n * 2)`
- **Consumo:** `intStream.forEach(System.out::println)`
- **Ordenamiento:** `intStream.sorted()`

#### Expresiones Lambda y Interfaces Funcionales

Las expresiones lambda permiten definir métodos anónimos y son una parte fundamental de la programación funcional en Java. Se utilizan comúnmente con interfaces funcionales.

**Ejemplo de Lambda con Stream:**

```java
import java.util.Arrays;
import java.util.List;

public class LambdaStreamExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Mango");
        
        // Filtrar y ordenar usando una expresión lambda
        frutas.stream()
              .filter(f -> f.startsWith("M"))
              .sorted((a, b) -> a.compareTo(b))
              .forEach(System.out::println); // Imprime "Mango"
    }
}
```

### Conclusión y Consideraciones Adicionales

El uso de Streams en Java, junto con expresiones lambda, proporciona una manera poderosa y eficiente de procesar datos de manera funcional. La capacidad de suministrar, filtrar, mapear, consumir y ordenar datos de manera fluida permite a los desarrolladores escribir código más limpio y mantenible.

Es fundamental entender el uso de Streams de objetos y primitivos, así como las operaciones clave y las interfaces funcionales que los soportan. Practicar con ejemplos variados y comprender las mejores prácticas en el manejo de datos utilizando Streams te preparará para manejar tareas complejas de procesamiento de datos en aplicaciones reales.