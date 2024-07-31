## Campos, Métodos y Constructores

### 1. Campos

Los campos son variables que se declaran dentro de una clase y representan el estado o las propiedades de los objetos de esa clase. Pueden ser de cualquier tipo de datos, incluyendo tipos primitivos y objetos.

**Declaración de campos:**
```java
public class Persona {
    String nombre; // Campo de instancia
    int edad; // Campo de instancia
    static int contador; // Campo estático
}
```
### 2. Métodos

Los métodos son bloques de código que realizan una tarea específica y se definen dentro de una clase. Pueden tomar argumentos, realizar operaciones y devolver valores.

**Declaración de métodos:**
```java
public class Calculadora {
    int sumar(int a, int b) {
        return a + b;
    }

    void imprimirSaludo() {
        System.out.println("¡Hola!");
    }
}
```
**Invocación de métodos:**
```java
public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        int resultado = calc.sumar(5, 3); // Invoca el método sumar
        System.out.println("Resultado: " + resultado); // Imprime: Resultado: 8
        calc.imprimirSaludo(); // Invoca el método imprimirSaludo
    }
}
```
### 3. Constructores

Los constructores son métodos especiales que se utilizan para inicializar objetos. Se llaman automáticamente cuando se crea una nueva instancia de una clase. Los constructores tienen el mismo nombre que la clase y no tienen un tipo de retorno.

**Declaración de constructores:**

*public class Persona {*
    *String nombre;*
    *int edad;*

    *// Constructor por defecto*
    *public Persona() {*
        *this.nombre = "Desconocido";*
        *this.edad = 0;*
    *}*

    *// Constructor parametrizado*
    *public Persona(String nombre, int edad) {*
        *this.nombre = nombre;*
        *this.edad = edad;*
    *}*
*}*

**Creación de objetos usando constructores:**

*public class Main {*
    *public static void main(String[] args) {*
        *Persona persona1 = new Persona(); // Llama al constructor por defecto*
        *Persona persona2 = new Persona("Juan", 25); // Llama al constructor parametrizado*

        *System.out.println("Persona 1: " + persona1.nombre + ", " + persona1.edad); // Imprime: Persona 1: Desconocido, 0*
        *System.out.println("Persona 2: " + persona2.nombre + ", " + persona2.edad); // Imprime: Persona 2: Juan, 25*
    *}*
*}*

### Ejemplos Completos

**Campos, métodos y constructores en una clase:**

```java
public class Persona {
    // Campos
    String nombre;
    int edad;

    // Constructor por defecto
    public Persona() {
        this.nombre = "Desconocido";
        this.edad = 0;
    }

    // Constructor parametrizado
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    // Método
    public void imprimirInfo() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }
}

public class Main {
    public static void main(String[] args) {
        // Crear objetos usando constructores
        Persona persona1 = new Persona();
        Persona persona2 = new Persona("Juan", 25);

        // Invocar métodos
        persona1.imprimirInfo(); // Imprime: Nombre: Desconocido, Edad: 0
        persona2.imprimirInfo(); // Imprime: Nombre: Juan, Edad: 25
    }
}
```

### Conclusión

Los campos, métodos y constructores son los bloques fundamentales de las clases en Java. Los campos almacenan el estado de los objetos, los métodos definen el comportamiento, y los constructores inicializan los objetos.

### Consideraciones Adicionales

- **Encapsulamiento:** Utiliza modificadores de acceso (`private`, `protected`, `public`) para controlar el acceso a los campos y métodos y proteger el estado interno de los objetos.
- **Sobrecarga de Constructores:** Java permite la sobrecarga de constructores, lo que facilita la creación de objetos con diferentes conjuntos de parámetros.
- **Métodos Estáticos:** Los métodos estáticos (de clase) no requieren una instancia de la clase y pueden acceder a campos estáticos.
- **Buenas Prácticas:** Es recomendable inicializar todos los campos, ya sea directamente en la declaración o mediante constructores, para evitar estados inconsistentes.
