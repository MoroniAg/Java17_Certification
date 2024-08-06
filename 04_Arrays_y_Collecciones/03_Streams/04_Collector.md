### `collect()` y `Collectors` en Java

El método `collect()` es una operación terminal en la API de Streams que transforma los elementos de un Stream en un contenedor diferente, como una lista, un conjunto o un mapa. La clase `Collectors` proporciona una variedad de métodos de fábrica que facilitan la colección de datos en diversas estructuras.

#### Uso de `collect()`

El método `collect()` toma un `Collector` como argumento y se utiliza para transformar los elementos del Stream en una estructura de datos final.

#### Ejemplos básicos de `collect()`

```java
import java.util.Arrays;
import java.util.List;
import java.util.Set;
import java.util.Map;
import java.util.stream.Collectors;

public class CollectExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza", "Manzana", "Mango");

        // Coleccionar en una lista
        List<String> listaFrutas = frutas.stream().collect(Collectors.toList());
        System.out.println(listaFrutas);  // [Manzana, Banana, Cereza, Manzana, Mango]

        // Coleccionar en un conjunto
        Set<String> conjuntoFrutas = frutas.stream().collect(Collectors.toSet());
        System.out.println(conjuntoFrutas);  // [Manzana, Banana, Cereza, Mango]

        // Coleccionar en un mapa
        Map<String, Integer> mapaFrutas = frutas.stream()
            .collect(Collectors.toMap(f -> f, f -> f.length(), (f1, f2) -> f1));
        System.out.println(mapaFrutas);  // {Banana=6, Cereza=6, Mango=5, Manzana=7}
    }
}
```

### Métodos Comunes de `Collectors`

#### `Collectors.toList()`

Convierte los elementos del Stream en una `List`.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ToListExample {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> listaNumeros = numeros.stream().collect(Collectors.toList());
        System.out.println(listaNumeros);  // [1, 2, 3, 4, 5]
    }
}
```

#### `Collectors.toSet()`

Convierte los elementos del Stream en un `Set`.

```java
import java.util.Arrays;
import java.util.Set;
import java.util.stream.Collectors;

public class ToSetExample {
    public static void main(String[] args) {
        Set<String> conjuntoFrutas = Arrays.stream(new String[]{"Manzana", "Banana", "Cereza", "Manzana"})
                                            .collect(Collectors.toSet());
        System.out.println(conjuntoFrutas);  // [Manzana, Banana, Cereza]
    }
}
```

#### `Collectors.toMap()`

Convierte los elementos del Stream en un `Map`.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class ToMapExample {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Banana", "Cereza");

        Map<String, Integer> mapaFrutas = frutas.stream()
            .collect(Collectors.toMap(f -> f, String::length));
        System.out.println(mapaFrutas);  // {Banana=6, Cereza=6, Manzana=7}
    }
}
```

#### `Collectors.joining()`

Concatena los elementos del Stream en un solo `String`.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class JoiningExample {
    public static void main(String[] args) {
        List<String> palabras = Arrays.asList("Java", "Streams", "API");

        String resultado = palabras.stream().collect(Collectors.joining(", "));
        System.out.println(resultado);  // Java, Streams, API
    }
}
```

#### `Collectors.groupingBy()`

Agrupa los elementos del Stream por una clasificación.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class GroupingByExample {
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

#### `Collectors.partitioningBy()`

Particiona los elementos del Stream en dos listas basadas en un predicado.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class PartitioningByExample {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        Map<Boolean, List<Integer>> particionadoPorPares = numeros.stream()
            .collect(Collectors.partitioningBy(n -> n % 2 == 0));

        System.out.println("Pares: " + particionadoPorPares.get(true));  // [2, 4, 6, 8, 10]
        System.out.println("Impares: " + particionadoPorPares.get(false));  // [1, 3, 5, 7, 9]
    }
}
```

### Conclusión y Consideraciones Adicionales

La combinación del método `collect()` y la clase `Collectors` permite una gran flexibilidad y poder al procesar datos en Streams. Conocer cómo usar estas herramientas eficientemente puede mejorar significativamente la calidad y la eficiencia del código. Los ejemplos prácticos y la experimentación con diferentes tipos de colecciones ayudarán a consolidar este conocimiento y a aplicarlo en proyectos del mundo real.


### Ejemplo 1: Filtrar y Agrupar Datos de una Base de Datos

Supongamos que tienes una lista de empleados y quieres agruparlos por departamento y luego particionarlos por si son empleados a tiempo completo o a tiempo parcial.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

class Empleado {
    String nombre;
    String departamento;
    boolean tiempoCompleto;

    Empleado(String nombre, String departamento, boolean tiempoCompleto) {
        this.nombre = nombre;
        this.departamento = departamento;
        this.tiempoCompleto = tiempoCompleto;
    }

    public String getDepartamento() {
        return departamento;
    }

    public boolean esTiempoCompleto() {
        return tiempoCompleto;
    }

    @Override
    public String toString() {
        return nombre;
    }
}

public class EjemploEmpleado {
    public static void main(String[] args) {
        List<Empleado> empleados = Arrays.asList(
            new Empleado("Juan", "IT", true),
            new Empleado("Ana", "HR", false),
            new Empleado("Pedro", "IT", false),
            new Empleado("Maria", "HR", true),
            new Empleado("Luis", "IT", true)
        );

        Map<String, Map<Boolean, List<Empleado>>> agrupadosPorDeptoYTiempo = empleados.stream()
            .collect(Collectors.groupingBy(Empleado::getDepartamento,
                Collectors.partitioningBy(Empleado::esTiempoCompleto)));

        agrupadosPorDeptoYTiempo.forEach((depto, particion) -> {
            System.out.println("Departamento: " + depto);
            System.out.println("Tiempo Completo: " + particion.get(true));
            System.out.println("Tiempo Parcial: " + particion.get(false));
        });
    }
}
```

### Ejemplo 2: Procesar Datos de un Archivo CSV

Imagina que tienes un archivo CSV con datos de productos y quieres agruparlos por categoría y luego convertir los nombres de los productos en una lista.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

class Producto {
    String nombre;
    String categoria;

    Producto(String nombre, String categoria) {
        this.nombre = nombre;
        this.categoria = categoria;
    }

    public String getCategoria() {
        return categoria;
    }

    @Override
    public String toString() {
        return nombre;
    }
}

public class EjemploProducto {
    public static void main(String[] args) {
        List<Producto> productos = Arrays.asList(
            new Producto("Laptop", "Electrónica"),
            new Producto("Celular", "Electrónica"),
            new Producto("Silla", "Muebles"),
            new Producto("Mesa", "Muebles"),
            new Producto("Televisor", "Electrónica")
        );

        Map<String, List<String>> productosPorCategoria = productos.stream()
            .collect(Collectors.groupingBy(Producto::getCategoria,
                Collectors.mapping(p -> p.nombre, Collectors.toList())));

        productosPorCategoria.forEach((categoria, nombres) -> {
            System.out.println("Categoría: " + categoria);
            System.out.println("Productos: " + nombres);
        });
    }
}
```

### Ejemplo 3: Análisis de Datos de Ventas

Supongamos que tienes una lista de ventas y quieres calcular el total de ventas por cada vendedor y luego particionar las ventas en mayores y menores a un cierto umbral.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

class Venta {
    String vendedor;
    double monto;

    Venta(String vendedor, double monto) {
        this.vendedor = vendedor;
        this.monto = monto;
    }

    public String getVendedor() {
        return vendedor;
    }

    public double getMonto() {
        return monto;
    }

    @Override
    public String toString() {
        return "Venta{" + "vendedor='" + vendedor + '\'' + ", monto=" + monto + '}';
    }
}

public class EjemploVenta {
    public static void main(String[] args) {
        List<Venta> ventas = Arrays.asList(
            new Venta("Carlos", 150.0),
            new Venta("Ana", 250.0),
            new Venta("Carlos", 300.0),
            new Venta("Ana", 100.0),
            new Venta("Luis", 200.0)
        );

        Map<String, Map<Boolean, List<Venta>>> ventasPorVendedorYUmbral = ventas.stream()
            .collect(Collectors.groupingBy(Venta::getVendedor,
                Collectors.partitioningBy(v -> v.getMonto() > 200)));

        ventasPorVendedorYUmbral.forEach((vendedor, particion) -> {
            System.out.println("Vendedor: " + vendedor);
            System.out.println("Ventas mayores a 200: " + particion.get(true));
            System.out.println("Ventas menores o iguales a 200: " + particion.get(false));
        });
    }
}
```

Estos ejemplos muestran cómo puedes aplicar los conceptos de `collect()` y `Collectors` en situaciones del mundo real para procesar y analizar datos de manera eficiente.