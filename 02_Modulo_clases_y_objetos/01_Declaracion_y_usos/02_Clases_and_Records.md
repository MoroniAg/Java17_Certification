## Crear Clases y Registros, y Definir y Usar Campos y Métodos de Instancia y Estáticos, Constructores, e Inicializadores

### Clases

En Java, una clase es una plantilla para crear objetos que define sus atributos (también llamados campos) y métodos. Las clases pueden tener constructores para inicializar sus objetos y pueden incluir campos y métodos estáticos.

**Definición de una Clase:**

```java
public class Persona {
    private String nombre;
    private int edad;

    // Constructor
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    // Método de instancia
    public void mostrarInformacion() {
        System.out.println("Nombre: " + nombre);
        System.out.println("Edad: " + edad);
    }
}
```

**Explicación:**
- **`nombre` y `edad`**: Campos de instancia que definen las propiedades del objeto `Persona`.
- **`Persona(String nombre, int edad)`**: Constructor que inicializa los atributos `nombre` y `edad`.
- **`mostrarInformacion()`**: Método de instancia que accede a los atributos del objeto y muestra la información.

### Registros `record` (Java 14+)

#### Definición y Sintaxis

Un registro en Java es una clase especial que se usa para representar un conjunto de datos inmutables. La sintaxis para definir un registro es bastante simple y se utiliza la palabra clave `record`.


Los registros (o `records`) son una característica introducida en Java 14 para crear tipos inmutables con un conjunto fijo de atributos. Los registros proporcionan automáticamente implementaciones de métodos como `equals()`, `hashCode()`, y `toString()`.

**Definición de un Registro:**

```java
public record Persona(String nombre, int edad) {
    // Los registros automáticamente proporcionan el constructor, getters, equals, hashCode, y toString
}
```

**Explicación:**
- **`Persona`**: El nombre del registro.
- **`String nombre, int edad`**: Los atributos del registro.
- Los registros generan automáticamente un constructor que toma los atributos como parámetros, así como métodos para obtener los valores y representaciones de los objetos.

- **`public record Persona(String nombre, int edad)`**: Define un registro llamado `Persona` con dos campos, `nombre` y `edad`.
- El compilador automáticamente proporciona un constructor, métodos de acceso, `equals()`, `hashCode()`, y `toString()`.


#### Componentes Automáticos

1. **Constructor:** Genera un constructor con todos los parámetros de los campos definidos en el registro.

   **Ejemplo:**
   ```java
   Persona persona = new Persona("Ana", 28);
   ```

2. **Métodos de Acceso:** Proporciona métodos públicos para obtener los valores de los campos. Estos métodos tienen el mismo nombre que los campos.

   **Ejemplo:**
   ```java
   String nombre = persona.nombre(); // "Ana"
   int edad = persona.edad();       // 28
   ```

3. **`toString()`:** Genera una representación en cadena de los valores de los campos.

   **Ejemplo:**
   ```java
   System.out.println(persona); // Persona[nombre=Ana, edad=28]
   ```

4. **`equals()`:** Implementa una comparación basada en los valores de los campos.

   **Ejemplo:**
   ```java
   Persona otraPersona = new Persona("Ana", 28);
   System.out.println(persona.equals(otraPersona)); // true
   ```

5. **`hashCode()`:** Genera un código hash basado en los valores de los campos.

   **Ejemplo:**
   ```java
   System.out.println(persona.hashCode()); // Hash code basado en nombre y edad
   ```

#### Métodos Adicionales

Puedes añadir métodos adicionales a un registro para proporcionar funcionalidad extra sin afectar a los métodos automáticos.

**Ejemplo:**

```java
public record Persona(String nombre, int edad) {
    public String saludo() {
        return "Hola, soy " + nombre + " y tengo " + edad + " años.";
    }
}
```

**Uso del Método Adicional:**

```java
Persona persona = new Persona("Luis", 32);
System.out.println(persona.saludo()); // Hola, soy Luis y tengo 32 años.
```

#### Métodos y Campos Estáticos

Los registros permiten definir métodos estáticos y campos estáticos, que no están relacionados con las instancias del registro.

**Ejemplo:**

```java
public record Persona(String nombre, int edad) {
    // Campo estático
    public static final String ESPECIE = "Homo sapiens";

    // Método estático
    public static void imprimirEspecie() {
        System.out.println("Especie: " + ESPECIE);
    }
}
```

**Uso de Método Estático:**

```java
Persona.imprimirEspecie(); // Especie: Homo sapiens
```

#### Bloques de Inicialización

Aunque los registros no permiten bloques de inicialización de instancia, puedes usar bloques de inicialización estáticos para configurar campos estáticos.

**Ejemplo:**

```java
public record Persona(String nombre, int edad) {
    // Inicializador estático
    static {
        System.out.println("Inicialización estática de Persona");
    }
}
```

**Ejecución:**

```java
Persona persona = new Persona("Maria", 25); // Inicialización estática de Persona
```

#### Conclusión y Consideraciones Adicionales

Los registros en Java simplifican la creación de tipos de datos inmutables, reduciendo el código boilerplate asociado a la creación de clases de datos. Proporcionan una manera elegante y eficiente de manejar datos, con un enfoque en la inmutabilidad y la claridad del código. Aprovechar las capacidades de los registros, como los métodos automáticos y la desestructuración, puede mejorar la eficiencia del desarrollo y la mantenibilidad del código.

#### Referencias

Oracle. (2023). Java Platform, Standard Edition 17 API Specification. Retrieved from [https://docs.oracle.com/en/java/javase/17/docs/api/index.html](https://docs.oracle.com/en/java/javase/17/docs/api/index.html).


### Campos de Instancia y Estáticos

- **Campos de Instancia**: Son variables que pertenecen a una instancia específica de una clase. Cada objeto creado a partir de la clase tiene su propia copia de estos campos.

- **Campos Estáticos**: Son variables compartidas por todas las instancias de una clase. Se definen con la palabra clave `static`.

**Ejemplo de Campos:**

```java
public class Ejemplo {
    private int instanciaCampo; // Campo de instancia
    private static int estaticoCampo; // Campo estático

    // Constructor de instancia
    public Ejemplo(int valor) {
        this.instanciaCampo = valor;
    }

    // Método de instancia
    public void metodoDeInstancia() {
        System.out.println("Campo de instancia: " + instanciaCampo);
    }

    // Método estático
    public static void metodoEstatico() {
        System.out.println("Campo estático: " + estaticoCampo);
    }
}
```

**Explicación:**
- **`instanciaCampo`**: Campo de instancia que pertenece a cada objeto `Ejemplo`.
- **`estaticoCampo`**: Campo estático que es compartido por todas las instancias de `Ejemplo`.
- **`metodoDeInstancia()`**: Método de instancia que opera sobre el campo de instancia.
- **`metodoEstatico()`**: Método estático que opera sobre el campo estático.

### Constructores

Los constructores son bloques de código que se ejecutan al crear una instancia de una clase. Su propósito principal es inicializar los atributos del objeto.

**Ejemplo de Constructores:**

```java
public class Ejemplo {
    private int valor;

    // Constructor sin parámetros
    public Ejemplo() {
        this.valor = 0;
    }

    // Constructor con parámetros
    public Ejemplo(int valor) {
        this.valor = valor;
    }
}
```

**Explicación:**
- **`Ejemplo()`**: Constructor sin parámetros que inicializa el campo `valor` a `0`.
- **`Ejemplo(int valor)`**: Constructor con parámetros que inicializa el campo `valor` con el valor proporcionado.

### Inicializadores de Instancia y Estáticos

- **Inicializadores de Instancia**: Bloques de código que se ejecutan cuando se crea una instancia de la clase. Se utilizan para inicializar campos de instancia.

- **Inicializadores Estáticos**: Bloques de código que se ejecutan cuando la clase se carga en la JVM. Se utilizan para inicializar campos estáticos.

**Ejemplo de Inicializadores:**

```java
public class Inicializador {
    private int valor;
    private static int staticValor;

    // Inicializador de instancia
    {
        valor = 10;
        System.out.println("Bloque de inicialización de instancia");
    }

    // Inicializador estático
    static {
        staticValor = 20;
        System.out.println("Bloque de inicialización estático");
    }

    public Inicializador() {
        System.out.println("Constructor de Inicializador");
    }
}
```

**Explicación:**
- **Bloque de Inicialización de Instancia (`{ ... }`)**: Se ejecuta cada vez que se crea una instancia de `Inicializador`, antes de ejecutar el constructor.
- **Bloque de Inicialización Estático (`static { ... }`)**: Se ejecuta una vez cuando la clase `Inicializador` se carga por primera vez en la JVM, antes de que se pueda crear cualquier instancia de la clase.

### Conclusión y Consideraciones Adicionales

Entender cómo crear y usar clases y registros, y cómo manejar campos y métodos de instancia y estáticos, es fundamental para la programación orientada a objetos en Java. Los constructores permiten inicializar objetos correctamente, y los inicializadores proporcionan un mecanismo adicional para configurar el estado inicial de los objetos y las clases. Este conocimiento es esencial para diseñar aplicaciones robustas y bien estructuradas.

### Referencias

Oracle. (2023). Java Platform, Standard Edition 17 API Specification. Retrieved from [https://docs.oracle.com/en/java/javase/17/docs/api/index.html](https://docs.oracle.com/en/java/javase/17/docs/api/index.html).