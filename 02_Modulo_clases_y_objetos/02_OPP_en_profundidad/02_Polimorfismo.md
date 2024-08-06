### Polimorfismo en Java 17

El polimorfismo es uno de los pilares fundamentales de la programación orientada a objetos, junto con la encapsulación y la herencia. En Java, el polimorfismo permite que una referencia a una clase se comporte de diferentes maneras dependiendo del contexto. Este comportamiento se logra principalmente a través de la herencia y la implementación de interfaces.

#### Tipos de Polimorfismo

1. **Polimorfismo en tiempo de compilación (sobrecarga de métodos)**:
   - Este tipo se logra mediante la sobrecarga de métodos, donde varios métodos en la misma clase tienen el mismo nombre pero diferentes parámetros.

2. **Polimorfismo en tiempo de ejecución (sobrescritura de métodos)**:
   - Se logra mediante la herencia y la sobrescritura de métodos. Permite que una subclase proporcione una implementación específica de un método que ya está definido en su superclase.

#### Polimorfismo en Tiempo de Ejecución

Este es el tipo de polimorfismo más común y poderoso en Java. A través de la sobrescritura de métodos, una subclase puede modificar la funcionalidad de un método heredado de la superclase. La JVM decide qué método invocar en tiempo de ejecución, basándose en el objeto al que apunta la referencia.

##### Ejemplo:

```java
class Animal {
    void makeSound() {
        System.out.println("Animal hace un sonido");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Perro ladra");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Gato maúlla");
    }
}

public class PolymorphismDemo {
    public static void main(String[] args) {
        Animal myAnimal = new Dog();
        myAnimal.makeSound();  // Output: Perro ladra
        
        myAnimal = new Cat();
        myAnimal.makeSound();  // Output: Gato maúlla
    }
}
```

En este ejemplo, aunque `myAnimal` es de tipo `Animal`, la JVM invoca el método `makeSound` de la clase a la que realmente apunta la referencia (`Dog` o `Cat`), demostrando polimorfismo en tiempo de ejecución.

#### Uso de Interfaces

Las interfaces son una herramienta poderosa para lograr polimorfismo. Permiten definir un contrato que las clases pueden implementar, garantizando que las clases proporcionen ciertas funcionalidades.

##### Ejemplo:

```java
interface Drawable {
    void draw();
}

class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Dibujar un círculo");
    }
}

class Square implements Drawable {
    @Override
    public void draw() {
        System.out.println("Dibujar un cuadrado");
    }
}

public class InterfacePolymorphismDemo {
    public static void main(String[] args) {
        Drawable shape = new Circle();
        shape.draw();  // Output: Dibujar un círculo
        
        shape = new Square();
        shape.draw();  // Output: Dibujar un cuadrado
    }
}
```

En este ejemplo, `shape` es una referencia de tipo `Drawable` que puede apuntar a cualquier objeto que implemente la interfaz `Drawable`.

#### Ventajas del Polimorfismo

1. **Flexibilidad y Extensibilidad**:
   - Permite escribir código más flexible y extensible, ya que los nuevos comportamientos pueden añadirse fácilmente mediante la herencia o la implementación de interfaces.
   
2. **Reutilización de Código**:
   - Promueve la reutilización de código mediante la generalización de métodos y clases.
   
3. **Intercambiabilidad**:
   - Los objetos de diferentes clases pueden ser tratados de manera uniforme, facilitando la intercambiabilidad de componentes.

#### Consideraciones Adicionales

- **Clases abstractas vs Interfaces**:
  - Las clases abstractas pueden contener una implementación parcial y ser heredadas por otras clases, mientras que las interfaces solo pueden declarar métodos (hasta Java 8), pero desde Java 8 pueden contener métodos predeterminados y estáticos.
  
- **Cohesión y Acoplamiento**:
  - El uso excesivo de polimorfismo puede llevar a un diseño de código poco cohesionado y altamente acoplado, por lo que es importante balancear su uso.

### Conclusión y Consideraciones Adicionales

El polimorfismo es crucial para la programación orientada a objetos en Java, permitiendo que el mismo código funcione con diferentes tipos de objetos. Este principio mejora la flexibilidad y mantenibilidad del código. Para dominar el polimorfismo en Java 17, es importante practicar con ejemplos complejos, integrar otros conceptos como la herencia y las interfaces, y entender profundamente cómo funciona la JVM en tiempo de ejecución.

Para profundizar, considera explorar:

- El impacto del polimorfismo en el rendimiento de la JVM.
- La integración del polimorfismo con otras características avanzadas de Java 17, como `record` y `sealed classes`.
- Ejemplos prácticos en aplicaciones reales y patrones de diseño que aprovechan el polimorfismo.

### Integración del Polimorfismo con Características Avanzadas de Java 17: `record` y `sealed classes`

Java 17 introduce características avanzadas como `record` y `sealed classes`, que mejoran la modelación de datos y el control sobre la jerarquía de clases, respectivamente. A continuación, se detalla cómo estas características se integran con el polimorfismo para crear diseños más robustos y seguros.

#### `record`

Los `record` son una nueva forma de definir clases de datos en Java. Proporcionan una sintaxis concisa para declarar clases que son principalmente "contenedores de datos". Aunque los `record` son inmutables por defecto, pueden participar en jerarquías polimórficas.

##### Ejemplo de `record`:

```java
public record Point(int x, int y) {}

public record ColoredPoint(int x, int y, String color) extends Point {
    public ColoredPoint(int x, int y, String color) {
        super(x, y);
        this.color = color;
    }
}
```

Aquí, `ColoredPoint` extiende `Point`, demostrando que los `record` pueden ser parte de jerarquías polimórficas. Sin embargo, dado que los `record` son finales por defecto, no pueden ser extendidos más allá de una capa.

#### `sealed classes`

Las `sealed classes` permiten restringir qué otras clases pueden extender o implementar una clase o interfaz. Esta característica proporciona un control más preciso sobre la jerarquía de tipos, mejorando la seguridad y claridad del diseño del código.

##### Ejemplo de `sealed classes`:

```java
public abstract sealed class Shape permits Circle, Square, Rectangle {
    public abstract double area();
}

public final class Circle extends Shape {
    private final double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

public final class Square extends Shape {
    private final double side;

    public Square(double side) {
        this.side = side;
    }

    @Override
    public double area() {
        return side * side;
    }
}

public final class Rectangle extends Shape {
    private final double length, width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    @Override
    public double area() {
        return length * width;
    }
}
```

En este ejemplo, `Shape` es una clase `sealed` que solo puede ser extendida por `Circle`, `Square` y `Rectangle`. Esto permite un control estricto sobre la jerarquía de clases, asegurando que solo las clases permitidas pueden ser instancias de `Shape`.

#### Integración del Polimorfismo con `record` y `sealed classes`

La combinación de polimorfismo con `record` y `sealed classes` permite crear jerarquías de clases más controladas y seguras. A continuación se muestra cómo se puede utilizar el polimorfismo con estas características:

##### Ejemplo completo:

```java
public sealed interface Drawable permits Circle, Square {
    void draw();
}

public record Circle(double radius) implements Drawable {
    @Override
    public void draw() {
        System.out.println("Dibujar un círculo con radio " + radius);
    }
}

public record Square(double side) implements Drawable {
    @Override
    public void draw() {
        System.out.println("Dibujar un cuadrado con lado " + side);
    }
}

public class Main {
    public static void main(String[] args) {
        Drawable shape1 = new Circle(5.0);
        Drawable shape2 = new Square(4.0);

        shape1.draw();  // Output: Dibujar un círculo con radio 5.0
        shape2.draw();  // Output: Dibujar un cuadrado con lado 4.0
    }
}
```

En este ejemplo, `Drawable` es una interfaz `sealed` que solo puede ser implementada por `Circle` y `Square`. Esto garantiza que solo esas dos clases pueden ser tratadas como `Drawable`, mejorando la seguridad y claridad del diseño del código.

### Conclusión y Consideraciones Adicionales

La integración de polimorfismo con `record` y `sealed classes` en Java 17 proporciona herramientas poderosas para diseñar jerarquías de clases seguras y manejables. Los `record` permiten crear clases de datos concisas y eficientes, mientras que las `sealed classes` controlan estrictamente qué clases pueden ser parte de una jerarquía, mejorando la seguridad y mantenibilidad del código.

Para profundizar en estos conceptos, se recomienda:

- Experimentar con ejemplos complejos que combinen `record`, `sealed classes`, y polimorfismo.
- Explorar patrones de diseño que se beneficien de estas características, como el patrón "Visitor".
- Revisar el impacto en el rendimiento y la compilación del uso de estas nuevas características.

