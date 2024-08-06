### Perform Decomposition, Concatenation and Reduction, and Grouping and Partitioning on Sequential and Parallel Streams

En este tema, cubriremos varias operaciones avanzadas que se pueden realizar con streams en Java, tanto secuenciales como paralelos.

#### Decomposition (Decomposición)

La descomposición se refiere a dividir un stream en múltiples partes. Aunque Java Streams no proporciona un método directo para dividir un stream en sub-streams, puedes usar el método `partitioningBy` de `Collectors` para dividir los datos en dos grupos basados en un predicado.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class StreamDecompositionExample {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        Map<Boolean, List<Integer>> particion = numeros.stream()
            .collect(Collectors.partitioningBy(n -> n % 2 == 0));

        System.out.println("Números pares: " + particion.get(true));  // [2, 4, 6, 8, 10]
        System.out.println("Números impares: " + particion.get(false));  // [1, 3, 5, 7, 9]
    }
}
```

#### Concatenation (Concatenación)

La concatenación de streams se puede realizar utilizando el método estático `Stream.concat`. Este método toma dos streams y los combina en uno solo.

```java
import java.util.stream.Stream;

public class StreamConcatenationExample {
    public static void main(String[] args) {
        Stream<String> stream1 = Stream.of("A", "B", "C");
        Stream<String> stream2 = Stream.of("D", "E", "F");

        Stream<String> concatenatedStream = Stream.concat(stream1, stream2);
        concatenatedStream.forEach(System.out::println);  // A, B, C, D, E, F
    }
}
```

#### Reduction (Reducción)

La reducción es una operación terminal que combina todos los elementos de un stream en un solo resultado. Los métodos más comunes de reducción son `reduce` y `collect`.

##### Reducción usando `reduce`

```java
import java.util.Arrays;
import java.util.List;

public class StreamReductionExample {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);

        int suma = numeros.stream()
            .reduce(0, Integer::sum);

        System.out.println("Suma: " + suma);  // Suma: 15
    }
}
```

##### Reducción usando `collect`

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamCollectExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");

        List<String> frutasMayusculas = frutas.stream()
            .map(String::toUpperCase)
            .collect(Collectors.toList());

        frutasMayusculas.forEach(System.out::println);  // MANZANA, BANANA, CEREZA
    }
}
```

#### Grouping (Agrupación)

La agrupación de elementos de un stream se puede realizar utilizando el método `groupingBy` de `Collectors`. Este método agrupa los elementos según una función de clasificación y devuelve un `Map`.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class StreamGroupingExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Melón", "Mango");

        Map<Character, List<String>> agrupadasPorPrimeraLetra = frutas.stream()
            .collect(Collectors.groupingBy(f -> f.charAt(0)));

        agrupadasPorPrimeraLetra.forEach((letra, lista) -> {
            System.out.println(letra + ": " + lista);
        });
        // M: [Manzana, Melón, Mango]
        // B: [Banana]
        // C: [Cereza]
    }
}
```

#### Partitioning (Particionamiento)

El particionamiento es similar a la agrupación, pero siempre resulta en un `Map` de dos listas basadas en un predicado. Esto se puede lograr con el método `partitioningBy` de `Collectors`.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class StreamPartitioningExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Melón", "Mango");

        Map<Boolean, List<String>> particionadoPorM = frutas.stream()
            .collect(Collectors.partitioningBy(f -> f.startsWith("M")));

        System.out.println("Empiezan con M: " + particionadoPorM.get(true));  // [Manzana, Melón, Mango]
        System.out.println("No empiezan con M: " + particionadoPorM.get(false));  // [Banana, Cereza]
    }
}
```

#### Streams Paralelos

Los streams paralelos permiten dividir el procesamiento de datos en varios subprocesos para mejorar el rendimiento en operaciones intensivas. Puedes convertir un stream secuencial en paralelo con el método `parallel`.

```java
import java.util.Arrays;
import java.util.List;

public class ParallelStreamExample {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        int sumaParalela = numeros.parallelStream()
            .reduce(0, Integer::sum);

        System.out.println("Suma Paralela: " + sumaParalela);  // Suma: 55
    }
}
```

### Conclusión y Consideraciones Adicionales

Comprender y dominar el uso de las operaciones avanzadas de Streams en Java es crucial para aprovechar al máximo esta poderosa API. Desde la descomposición y concatenación hasta la reducción, agrupación y particionamiento, cada operación tiene su lugar y propósito en el procesamiento de datos.

El uso de Streams paralelos puede mejorar significativamente el rendimiento en escenarios de gran volumen de datos, pero es importante tener en cuenta las consideraciones de concurrencia y la sobrecarga de gestión de hilos. Practicar con diversos ejemplos y casos de uso ayudará a entender mejor cómo aplicar estas técnicas en situaciones del mundo real, asegurando un código más eficiente y mantenible.