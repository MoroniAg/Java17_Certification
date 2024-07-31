## Sobrecarga de Métodos y Constructores

### 1. Sobrecarga de Métodos

La sobrecarga de métodos en Java permite definir múltiples métodos con el mismo nombre pero diferentes parámetros (tipo, número o ambos). Esto mejora la legibilidad del código y permite ofrecer distintas formas de invocar un método.

**Ejemplo de sobrecarga de métodos:**
```java
public class Calculadora {
    int sumar(int a, int b) {
        return a + b;
    }

    int sumar(int a, int b, int c) {
        return a + b + c;
    }

    double sumar(double a, double b) {
        return a + b;
    }
}
```
**Invocación de métodos sobrecargados:**
```java
public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();

        int resultado1 = calc.sumar(2, 3); // Llama al método sumar(int, int)
        int resultado2 = calc.sumar(1, 2, 3); // Llama al método sumar(int, int, int)
        double resultado3 = calc.sumar(2.5, 3.5); // Llama al método sumar(double, double)

        System.out.println("Resultado 1: " + resultado1); // Imprime: Resultado 1: 5
        System.out.println("Resultado 2: " + resultado2); // Imprime: Resultado 2: 6
        System.out.println("Resultado 3: " + resultado3); // Imprime: Resultado 3: 6.0
    }
}
```
### 2. Sobrecarga de Constructores

La sobrecarga de constructores permite definir múltiples constructores en una clase, cada uno con diferentes parámetros. Esto proporciona flexibilidad al crear objetos con diferentes inicializaciones.

**Ejemplo de sobrecarga de constructores:**
```java
public class Persona {
    String nombre;
    int edad;

    public Persona() {
        this.nombre = "Desconocido";
        this.edad = 0;
    }

    public Persona(String nombre) {
        this.nombre = nombre;
        this.edad = 0;
    }

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}
```
**Creación de objetos usando constructores sobrecargados:**
```java
public class Main {
    public static void main(String[] args) {
        Persona persona1 = new Persona(); // Llama al constructor por defecto
        Persona persona2 = new Persona("Juan"); // Llama al constructor con un parámetro
        Persona persona3 = new Persona("Ana", 30); // Llama al constructor con dos parámetros

        System.out.println("Persona 1: " + persona1.nombre + ", " + persona1.edad); // Imprime: Persona 1: Desconocido, 0
        System.out.println("Persona 2: " + persona2.nombre + ", " + persona2.edad); // Imprime: Persona 2: Juan, 0
        System.out.println("Persona 3: " + persona3.nombre + ", " + persona3.edad); // Imprime: Persona 3: Ana, 30
    }
}
```
### Ejemplos Completos

**Sobrecarga de métodos en una clase:**

```java
public class Calculadora {
    int sumar(int a, int b) {
        return a + b;
    }

    int sumar(int a, int b, int c) {
        return a + b + c;
    }

    double sumar(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();

        int resultado1 = calc.sumar(2, 3);
        int resultado2 = calc.sumar(1, 2, 3);
        double resultado3 = calc.sumar(2.5, 3.5);

        System.out.println("Resultado 1: " + resultado1);
        System.out.println("Resultado 2: " + resultado2);
        System.out.println("Resultado 3: " + resultado3);
    }
}
```

**Sobrecarga de constructores en una clase:**

```java
public class Persona {
    String nombre;
    int edad;

    public Persona() {
        this.nombre = "Desconocido";
        this.edad = 0;
    }

    public Persona(String nombre) {
        this.nombre = nombre;
        this.edad = 0;
    }

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}

public class Main {
    public static void main(String[] args) {
        Persona persona1 = new Persona();
        Persona persona2 = new Persona("Juan");
        Persona persona3 = new Persona("Ana", 30);

        System.out.println("Persona 1: " + persona1.nombre + ", " + persona1.edad);
        System.out.println("Persona 2: " + persona2.nombre + ", " + persona2.edad);
        System.out.println("Persona 3: " + persona3.nombre + ", " + persona3.edad);
    }
}
```

### Conclusión

La sobrecarga de métodos y constructores proporciona flexibilidad y mejora la legibilidad del código al permitir múltiples formas de invocar métodos y crear objetos con diferentes inicializaciones.

### Consideraciones Adicionales

- **Distinción de Parámetros:** Asegúrate de que los métodos y constructores sobrecargados se distingan claramente por sus parámetros (tipo, número o ambos) para evitar ambigüedades.
- **Uso Apropiado:** Utiliza la sobrecarga para proporcionar alternativas convenientes y claras para las operaciones y la creación de objetos.
- **Legibilidad:** Mantén la sobrecarga sencilla y evita complicarla con demasiadas variantes que puedan confundir a los desarrolladores que lean tu código.
