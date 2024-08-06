### Funciones Relacionadas a la Clase Stream en Java

Java Streams es una API que permite el procesamiento de datos de manera funcional. La clase `Stream` en Java proporciona una variedad de métodos que se pueden agrupar en operaciones intermedias y terminales.

#### Operaciones Intermedias

Las operaciones intermedias son aquellas que devuelven un nuevo Stream y permiten el encadenamiento de operaciones. Algunas de las operaciones intermedias más comunes incluyen:

##### `filter(Predicate<? super T> predicate)`

Filtra los elementos del Stream según un predicado.

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

##### `map(Function<? super T, ? extends R> mapper)`

Aplica una función a cada elemento del Stream y devuelve un Stream de los resultados.

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

##### `flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)`

Aplica una función a cada elemento del Stream, que a su vez produce un Stream de nuevos elementos. Los Streams resultantes se aplanan en un solo Stream.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamFlatMapExample {
    public static void main(String[] args) {
        List<List<String>> listaDeListas = Arrays.asList(
            Arrays.asList("Manzana", "Banana"),
            Arrays.asList("Cereza", "Mango")
        );
        
        List<String> listaPlano = listaDeListas.stream()
                                               .flatMap(List::stream)
                                               .collect(Collectors.toList());
        
        listaPlano.forEach(System.out::println); // Imprime cada fruta en una línea separada
    }
}
```

##### `distinct()`

Devuelve un Stream que contiene elementos distintos (sin duplicados) según el método `equals`.

```java
import java.util.Arrays;
import java.util.List;

public class StreamDistinctExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Manzana");
        
        frutas.stream()
              .distinct()
              .forEach(System.out::println); // Imprime "Manzana", "Banana", "Cereza"
    }
}
```

##### `sorted()`

Devuelve un Stream con los elementos ordenados de acuerdo con el orden natural.

```java
import java.util.Arrays;
import java.util.List;

public class StreamSortedExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Mango", "Banana", "Cereza", "Manzana");
        
        frutas.stream()
              .sorted()
              .forEach(System.out::println); // Imprime las frutas en orden alfabético
    }
}
```

##### `peek(Consumer<? super T> action)`

Devuelve un Stream compuesto de los elementos de este Stream, realizando la acción dada en cada elemento a medida que se consume.

```java
import java.util.Arrays;
import java.util.List;

public class StreamPeekExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Mango");
        
        frutas.stream()
              .peek(f -> System.out.println("Procesando: " + f))
              .sorted()
              .forEach(System.out::println);
    }
}
```

#### Operaciones Terminales

Las operaciones terminales producen un resultado o efecto secundario y cierran el Stream. Algunas operaciones terminales comunes incluyen:

##### `forEach(Consumer<? super T> action)`

Realiza una acción sobre cada elemento del Stream.

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

##### `collect(Collector<? super T, A, R> collector)`

Acumula los elementos del Stream en una colección o en otro tipo de resultado.

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
        
        frutasMayusculas.forEach(System.out::println); // Imprime las frutas en mayúsculas
    }
}
```

##### `reduce(BinaryOperator<T> accumulator)`

Combina los elementos del Stream en un solo resultado, utilizando un acumulador.

```java
import java.util.Arrays;
import java.util.List;

public class StreamReduceExample {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
        
        int suma = numeros.stream()
                          .reduce(0, Integer::sum);
        
        System.out.println("Suma: " + suma); // Imprime la suma de los números
    }
}
```

##### `count()`

Devuelve el número de elementos en el Stream.

```java
import java.util.Arrays;
import java.util.List;

public class StreamCountExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");
        
        long cantidad = frutas.stream().count();
        
        System.out.println("Cantidad de frutas: " + cantidad); // Imprime 3
    }
}
```

##### `findFirst()`

Devuelve un `Optional` con el primer elemento del Stream, si está presente.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class StreamFindFirstExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");
        
        Optional<String> primeraFruta = frutas.stream().findFirst();
        
        primeraFruta.ifPresent(System.out::println); // Imprime "Manzana"
    }
}
```

##### `findAny()`

Devuelve un `Optional` con algún elemento del Stream, si está presente. Es útil en operaciones paralelas.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class StreamFindAnyExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");
        
        Optional<String> algunaFruta = frutas.stream().findAny();
        
        algunaFruta.ifPresent(System.out::println); // Imprime alguna fruta del Stream
    }
}
```

##### `anyMatch(Predicate<? super T> predicate)`

Devuelve `true` si algún elemento del Stream coincide con el predicado.

```java
import java.util.Arrays;
import java.util.List;

public class StreamAnyMatchExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");
        
        boolean hayManzana = frutas.stream().anyMatch(f -> f.equals("Manzana"));
        
        System.out.println("Hay Manzana: " + hayManzana); // Imprime true
    }
}
```

##### `allMatch(Predicate<? super T> predicate)`

Devuelve `true` si todos los elementos del Stream coinciden con el predicado.

```java
import java.util.Arrays;
import java.util.List;

public class StreamAllMatchExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Mango", "Melón");
        
        boolean todasConM = frutas.stream().allMatch(f -> f.startsWith("M"));
        
        System.out.println("Todas las frutas empiezan con M: " + todasConM); // Imprime true
    }
}
```

##### `noneMatch(Predicate<? super T> predicate)`

Devuelve `true` si ningún elemento del Stream coincide con el predicado.

```java
import java.util.Arrays;
import java.util.List;

public class StreamNoneMatchExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");
        
        boolean ningunaConZ = frutas.stream().noneMatch(f -> f.startsWith("Z"));
        
        System.out.println("Ninguna fruta empieza con Z: " + ningunaConZ); // Imprime true
    }
}
```

### Conclusión y Consideraciones Adicionales



La API de Streams en Java proporciona un conjunto rico y variado de operaciones para procesar datos de manera eficiente y expresiva. Desde operaciones intermedias como `filter`, `map` y `sorted`, hasta operaciones terminales como `forEach`, `collect` y `reduce`, los Streams permiten manejar grandes volúmenes de datos con un código conciso y legible.

Para dominar el uso de Streams, es fundamental practicar con diversos ejemplos y casos de uso, comprendiendo cómo cada método puede ser aplicado en diferentes contextos. Además, es crucial tener en cuenta el impacto en el rendimiento y asegurarse de que las operaciones de Streams se utilizan de manera adecuada para aprovechar al máximo su potencial en aplicaciones Java.