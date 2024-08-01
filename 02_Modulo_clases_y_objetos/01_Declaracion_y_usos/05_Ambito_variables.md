### Entender los Ámbitos de las Variables, Usar Inferencia de Tipos en Variables Locales, Aplicar Encapsulamiento y Hacer Objetos Inmutables

#### Ámbitos de las Variables

En Java, el ámbito de una variable es la parte del programa donde la variable puede ser referenciada. Existen varios tipos de ámbitos:

**1. Ámbito de Variables Locales:**

Las variables locales son declaradas dentro de un método y solo pueden ser utilizadas dentro de ese método. No tienen valores predeterminados y deben ser inicializadas antes de usarlas.

*Ejemplo:*

```java
public void metodo() {
    int local = 10; // Variable local
    System.out.println(local);
    if (local > 5) {
        int otraLocal = 20; // Ámbito dentro del bloque if
        System.out.println(otraLocal);
    }
    // System.out.println(otraLocal); // Error: fuera del ámbito de otraLocal
}
```

**2. Ámbito de Variables de Instancia:**

Las variables de instancia son declaradas dentro de una clase pero fuera de cualquier método. Estas variables son accesibles para todos los métodos de la clase y se inicializan con valores predeterminados (0 para números, false para booleanos, null para objetos).

*Ejemplo:*

```java
public class Ejemplo {
    private int instancia; // Variable de instancia

    public void metodo() {
        instancia = 5;
    }

    public int obtenerInstancia() {
        return instancia;
    }
}
```

**3. Ámbito de Variables de Clase (Estáticas):**

Las variables de clase son declaradas con la palabra clave `static` y son compartidas entre todas las instancias de la clase. También se inicializan con valores predeterminados.

*Ejemplo:*

```java
public class Ejemplo {
    private static int clase; // Variable de clase

    public static void metodo() {
        clase = 5;
    }

    public static int obtenerClase() {
        return clase;
    }
}
```

#### Inferencia de Tipos en Variables Locales

Desde Java 10, se puede utilizar la palabra clave `var` para permitir que el compilador infiera el tipo de una variable local. Esta característica se llama "inferencia de tipo local" y mejora la legibilidad del código.

*Ejemplo:*

```java
public void metodo() {
    var texto = "Hola"; // Inferencia de tipo, 'texto' es de tipo String
    var numero = 10;    // Inferencia de tipo, 'numero' es de tipo int
    var lista = new ArrayList<String>(); // Inferencia de tipo, 'lista' es de tipo ArrayList<String>
    
    // Uso en un bucle for
    for (var elemento : lista) {
        System.out.println(elemento);
    }
}
```

### Aplicar Encapsulamiento

El encapsulamiento es un principio fundamental de la programación orientada a objetos que restringe el acceso directo a algunos de los componentes de un objeto. Esto se logra mediante el uso de modificadores de acceso (private, protected, public). El objetivo es proteger los datos y mantener un control sobre cómo se accede y modifica el estado del objeto.

*Ejemplo:*

```java
public class Persona {
    private String nombre; // Campo encapsulado
    private int edad;

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        if (nombre != null && !nombre.isEmpty()) {
            this.nombre = nombre;
        }
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        if (edad > 0) {
            this.edad = edad;
        }
    }
}
```

En este ejemplo, los campos `nombre` y `edad` son privados, lo que significa que no pueden ser accedidos directamente desde fuera de la clase. En su lugar, se utilizan métodos públicos (`getNombre`, `setNombre`, `getEdad`, `setEdad`) para acceder y modificar estos campos.

### Hacer Objetos Inmutables

Un objeto inmutable es aquel cuyo estado no puede ser modificado después de su creación. La inmutabilidad es útil para asegurar que los objetos sean seguros para su uso concurrente y para simplificar el razonamiento sobre el estado del programa.

Para hacer un objeto inmutable, se deben seguir varias prácticas:

1. Declarar todos los campos como `final`.
2. No proporcionar métodos que modifiquen los campos.
3. Asegurarse de que los campos no sean modificables y no expongan referencias internas mutables.

*Ejemplo:*

```java
public final class Persona {
    private final String nombre;
    private final int edad;

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    public String getNombre() {
        return nombre;
    }

    public int getEdad() {
        return edad;
    }

    // No hay métodos setters
}
```

En este ejemplo, la clase `Persona` es inmutable. Los campos `nombre` y `edad` son finales y solo pueden ser establecidos en el constructor. No hay métodos setters, por lo que una vez que se crea una instancia de `Persona`, su estado no puede ser modificado.

### Conclusión y Consideraciones Adicionales

Entender los diferentes ámbitos de las variables es crucial para controlar su visibilidad y duración. La inferencia de tipos puede simplificar el código y mejorar su legibilidad, aunque debe ser usada con cuidado para mantener la claridad. El encapsulamiento es esencial para mantener la integridad de los datos y la encapsulación. La inmutabilidad, aunque no siempre necesaria, puede ser una poderosa herramienta para crear objetos más seguros y fáciles de razonar.

### Referencias

Oracle. (2023). Java Platform, Standard Edition 17 API Specification. Retrieved from [https://docs.oracle.com/en/java/javase/17/docs/api/index.html](https://docs.oracle.com/en/java/javase/17/docs/api/index.html).