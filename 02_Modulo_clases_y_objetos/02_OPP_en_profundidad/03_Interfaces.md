### Crear y Usar Interfaces, Identificar Interfaces Funcionales y Utilizar Métodos Privados, Estáticos y Predeterminados en Interfaces

#### Interfaces en Java

Una interfaz en Java es un tipo abstracto que permite a las clases implementar métodos específicos. Las interfaces son fundamentales para la programación orientada a objetos en Java, ya que permiten la definición de un contrato que las clases deben seguir.

**Características de las interfaces:**
- Pueden contener métodos abstractos (sin implementación), métodos predeterminados (con implementación), métodos estáticos y métodos privados.
- No pueden contener campos de instancia, solo constantes (`static final`).
- Una clase puede implementar múltiples interfaces.

**Ejemplo básico de interfaz:**

```java
public interface Animal {
    void hacerSonido(); // Método abstracto
}
```

**Implementación de una interfaz:**

```java
public class Perro implements Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Ladrido");
    }
}
```

#### Interfaces Funcionales

Una interfaz funcional es una interfaz que contiene exactamente un método abstracto. Estas interfaces son fundamentales para trabajar con expresiones lambda y referencias a métodos. Java proporciona varias interfaces funcionales en el paquete `java.util.function`.

**Ejemplo de interfaz funcional:**

```java
@FunctionalInterface
public interface Operacion {
    int calcular(int a, int b);
}
```

**Uso de una interfaz funcional con una expresión lambda:**

```java
public class Main {
    public static void main(String[] args) {
        Operacion suma = (a, b) -> a + b;
        System.out.println(suma.calcular(5, 3)); // Salida: 8
    }
}
```

#### Métodos Predeterminados en Interfaces

Los métodos predeterminados (`default`) permiten proporcionar una implementación por defecto en las interfaces. Esto es útil para añadir nuevos métodos a interfaces existentes sin romper las clases que las implementan.

**Ejemplo de método predeterminado:**

```java
public interface Animal {
    void hacerSonido();

    default void dormir() {
        System.out.println("El animal está durmiendo");
    }
}
```

**Uso de método predeterminado:**

```java
public class Perro implements Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Ladrido");
    }
}

public class Main {
    public static void main(String[] args) {
        Perro perro = new Perro();
        perro.hacerSonido(); // Salida: Ladrido
        perro.dormir();      // Salida: El animal está durmiendo
    }
}
```

#### Métodos Estáticos en Interfaces

Los métodos estáticos en interfaces son similares a los métodos estáticos en clases. No pueden ser sobrescritos por las clases que implementan la interfaz.

**Ejemplo de método estático:**

```java
public interface Utilidades {
    static int sumar(int a, int b) {
        return a + b;
    }
}
```

**Uso de método estático:**

```java
public class Main {
    public static void main(String[] args) {
        int resultado = Utilidades.sumar(5, 3);
        System.out.println(resultado); // Salida: 8
    }
}
```

#### Métodos Privados en Interfaces

Introducidos en Java 9, los métodos privados en interfaces permiten compartir código entre los métodos predeterminados y estáticos de la interfaz sin exponerlos a las clases que implementan la interfaz.

**Ejemplo de método privado:**

```java
public interface Utilidades {
    static int sumar(int a, int b) {
        return a + b;
    }

    default int sumarTres(int a, int b, int c) {
        return sumar(a, b) + c;
    }

    private static int sumar(int a, int b) {
        return a + b;
    }
}
```

**Uso de método privado:**

```java
public class Main {
    public static void main(String[] args) {
        Utilidades utilidades = new Utilidades() {}; // Clase anónima
        int resultado = utilidades.sumarTres(1, 2, 3);
        System.out.println(resultado); // Salida: 6
    }
}
```

### Conclusión y Consideraciones Adicionales

Las interfaces en Java son una herramienta poderosa para definir contratos que las clases deben seguir, permitiendo una mayor flexibilidad y reutilización del código. Las interfaces funcionales facilitan el uso de expresiones lambda y referencias a métodos, mejorando la concisión y claridad del código. Los métodos predeterminados y estáticos en interfaces permiten la evolución de interfaces sin romper el código existente, y los métodos privados facilitan la reutilización de código dentro de la interfaz misma.

Es crucial comprender y practicar el uso de interfaces y sus métodos para aprovechar al máximo las capacidades de Java en el desarrollo orientado a objetos.

### Referencias

Oracle. (2023). Java Platform, Standard Edition 17 API Specification. Retrieved from [https://docs.oracle.com/en/java/javase/17/docs/api/index.html](https://docs.oracle.com/en/java/javase/17/docs/api/index.html).


### Métodos Privados en Interfaces

Introducidos en Java 9, los métodos privados en interfaces permiten compartir código entre los métodos predeterminados y estáticos de la interfaz sin exponerlos a las clases que implementan la interfaz. Esto mejora la reutilización del código dentro de la interfaz misma, manteniendo al mismo tiempo la encapsulación.

#### Características de los Métodos Privados en Interfaces

1. **Accesibilidad**: Los métodos privados en una interfaz solo pueden ser llamados por otros métodos predeterminados o estáticos dentro de la misma interfaz.
2. **Encapsulación**: Permiten ocultar la lógica interna de la interfaz, lo que mejora la mantenibilidad y la claridad del código.
3. **Reutilización de Código**: Facilitan la reutilización de la lógica común entre múltiples métodos de la interfaz.

#### Ejemplo de Uso de Métodos Privados en Interfaces

Supongamos que tenemos una interfaz `Utilidades` que realiza varias operaciones matemáticas. En lugar de duplicar la lógica para sumar números en varios métodos predeterminados y estáticos, podemos encapsular esa lógica en un método privado.

**Definición de la interfaz con métodos privados:**

```java
public interface Utilidades {

    // Método estático que llama al método privado
    static int sumar(int a, int b) {
        return sumarPrivado(a, b);
    }

    // Método predeterminado que llama al método privado
    default int sumarTres(int a, int b, int c) {
        return sumarPrivado(a, b) + c;
    }

    // Método privado para sumar dos números
    private static int sumarPrivado(int a, int b) {
        return a + b;
    }
}
```

En este ejemplo, el método privado `sumarPrivado` encapsula la lógica de sumar dos números. Este método privado es reutilizado tanto por el método estático `sumar` como por el método predeterminado `sumarTres`.

**Uso de la interfaz en una clase:**

```java
public class Main {
    public static void main(String[] args) {
        // Llamada al método estático directamente desde la interfaz
        int resultado1 = Utilidades.sumar(5, 3);
        System.out.println(resultado1); // Salida: 8

        // Uso del método predeterminado a través de una clase anónima que implementa la interfaz
        Utilidades utilidades = new Utilidades() {};
        int resultado2 = utilidades.sumarTres(1, 2, 3);
        System.out.println(resultado2); // Salida: 6
    }
}
```

### Beneficios de los Métodos Privados en Interfaces

1. **Reducción de Duplicación de Código**: Al encapsular la lógica común en métodos privados, se reduce la duplicación de código, lo que hace que el mantenimiento sea más fácil y menos propenso a errores.
2. **Claridad del Código**: Los métodos privados permiten que los métodos predeterminados y estáticos sean más concisos y legibles, ya que la lógica detallada se oculta en métodos privados.
3. **Encapsulación Mejorada**: Mantener la lógica dentro de la interfaz sin exponerla a las clases que implementan la interfaz mejora la encapsulación y seguridad del código.

### Consideraciones Adicionales

1. **Limitaciones**: Los métodos privados solo pueden ser llamados desde otros métodos dentro de la misma interfaz y no están disponibles para las clases que implementan la interfaz.
2. **Compatibilidad**: La capacidad de usar métodos privados en interfaces está disponible a partir de Java 9. Si se trabaja en un entorno con versiones anteriores de Java, esta característica no estará disponible.

### Conclusión

Los métodos privados en interfaces son una característica poderosa que mejora la capacidad de reutilización del código y la encapsulación en Java. Al comprender y utilizar estos métodos, los desarrolladores pueden crear interfaces más robustas y mantenibles, mejorando la calidad general del código.

### Referencias

Oracle. (2023). Java Platform, Standard Edition 17 API Specification. Retrieved from [https://docs.oracle.com/en/java/javase/17/docs/api/index.html](https://docs.oracle.com/en/java/javase/17/docs/api/index.html).