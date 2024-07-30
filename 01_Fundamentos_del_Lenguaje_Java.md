## Declaraciones, Bloques y Ámbito

### Declaraciones

En Java, las declaraciones son fundamentales para definir y utilizar variables, métodos, y clases. Cada declaración tiene una sintaxis específica y un propósito dentro del código.

**Declaración de Variables**

Las variables en Java se deben declarar con un tipo de datos que define el tipo de valor que pueden almacenar. Además de su tipo y nombre, se pueden inicializar con un valor.

```java
int edad = 30; // Declaración e inicialización
double salario; // Solo declaración
```

Las variables pueden ser de diferentes tipos:

- **Primitivos:** `int`, `char`, `double`, etc.
- **Referencia:** `String`, `ArrayList`, etc.

**Declaración de Métodos**

Los métodos en Java se declaran con un tipo de retorno, un nombre y una lista de parámetros. El método puede ser `public`, `private`, `protected`, o de acceso por defecto.

```java
public int sumar(int a, int b) {
    return a + b;
}
```

**Declaración de Clases**

Las clases en Java se definen utilizando la palabra clave `class`. Una clase puede contener campos (variables de instancia), métodos, y constructores.

```java
public class Vehiculo {
    String marca;
    int año;

    public void mostrarDetalles() {
        System.out.println("Marca: " + marca + ", Año: " + año);
    }
}
```

### Bloques

Los bloques en Java son secciones de código delimitadas por llaves `{}`. Existen varios tipos de bloques:

**Bloque de Clase**

El bloque de clase contiene las declaraciones de variables y métodos que definen el comportamiento y el estado de la clase.

```java
public class Ejemplo {
    int numero; // Variable de instancia

    void metodo() {
        // Código del método
    }
}
```

**Bloque de Método**

El bloque de método es donde se ejecuta el código cuando se llama al método. Los bloques de método pueden incluir variables locales, expresiones y otros bloques.

```java
public void ejecutar() {
    int resultado = 0; // Variable local
    for (int i = 0; i < 10; i++) {
        resultado += i;
    }
}
```

**Bloque de Inicialización**

Los bloques de inicialización se utilizan para ejecutar código cuando se crea una instancia de una clase o cuando la clase se carga.

- **Bloque de Inicialización Estático:** Se ejecuta una vez cuando la clase se carga por primera vez. Utilizado para inicializar variables estáticas.

  ```java
  static {
      System.out.println("Bloque estático ejecutado.");
  }
  ```

- **Bloque de Inicialización de Instancia:** Se ejecuta cada vez que se crea una nueva instancia de la clase, antes del constructor.

  ```java
  {
      System.out.println("Bloque de instancia ejecutado.");
  }
  ```

### Ámbito

El ámbito en Java determina la visibilidad y el ciclo de vida de las variables, métodos y clases. Se puede categorizar en:

**Ámbito de Clase**

Las variables de instancia y métodos definidos en una clase tienen un ámbito de clase. Estas variables y métodos pueden ser accedidos desde cualquier método dentro de la clase.

```java
public class Ejemplo {
    int variableDeInstancia; // Ámbito de clase

    void metodo() {
        System.out.println(variableDeInstancia);
    }
}
```

**Ámbito de Método**

Las variables locales a un método son accesibles solo dentro del método en el que están declaradas. Una vez que el método termina su ejecución, estas variables son destruidas.

```java
public void metodo() {
    int variableLocal = 10; // Ámbito del método
    System.out.println(variableLocal);
}
```

**Ámbito de Bloque**

Las variables declaradas dentro de un bloque de código (como dentro de un bucle o condicional) solo son accesibles dentro de ese bloque.

```java
public void metodo() {
    for (int i = 0; i < 5; i++) {
        int variableDeBucle = i; // Ámbito del bucle
        System.out.println(variableDeBucle);
    }
    // variableDeBucle no está accesible aquí
}
```

**Ámbito de Parámetro**

Los parámetros de métodos tienen un ámbito local al método y están disponibles solo dentro del método.

```java
public void metodo(int parametro) {
    System.out.println(parametro); // Ámbito del parámetro
}
```

### Ejemplo Completo

```java
public class Persona {
    String nombre; // Variable de instancia

    // Bloque de inicialización de instancia
    {
        nombre = "Desconocido";
    }

    // Bloque estático
    static {
        System.out.println("Clase Persona cargada.");
    }

    public Persona(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, mi nombre es " + nombre);
    }

    public void edad(int edad) {
        int añoActual = 2024; // Variable local
        int añoNacimiento = añoActual - edad;
        System.out.println("Año de nacimiento: " + añoNacimiento);
    }
}
```

