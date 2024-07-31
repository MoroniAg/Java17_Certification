## Herencia y Polimorfismo

### 1. Herencia

La herencia es un mecanismo fundamental en la programación orientada a objetos que permite a una clase derivar o heredar las propiedades y métodos de otra clase. La clase que hereda se llama subclase o clase derivada, y la clase de la que se hereda se llama superclase o clase base.

**Ejemplo de herencia:**
```java
public class Animal {
    public void hacerSonido() {
        System.out.println("El animal hace un sonido");
    }
}

public class Perro extends Animal {
    public void hacerSonido() {
        System.out.println("El perro ladra");
    }
}
```
### 2. Polimorfismo

El polimorfismo permite que un objeto tome muchas formas. En el contexto de la herencia, significa que una subclase puede ser tratada como una instancia de su superclase. Hay dos tipos principales de polimorfismo en Java:

#### Polimorfismo en tiempo de compilación (Sobrecarga de métodos)
Este tipo de polimorfismo se resuelve durante la compilación. Se logra mediante la sobrecarga de métodos.

**Ejemplo:**
```java
public class Calculadora {
    public int sumar(int a, int b) {
        return a + b;
    }

    public double sumar(double a, double b) {
        return a + b;
    }
}
```
#### Polimorfismo en tiempo de ejecución (Sobreescritura de métodos)
Este tipo de polimorfismo se resuelve durante la ejecución. Se logra mediante la sobreescritura de métodos, donde una subclase proporciona una implementación específica de un método que ya está definido en su superclase.

**Ejemplo de sobreescritura de métodos:**
```java
public class Animal {
    public void hacerSonido() {
        System.out.println("El animal hace un sonido");
    }
}

public class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("El perro ladra");
    }
}
```
### Ejemplos Completos

**Herencia y polimorfismo:**
```java
public class Animal {
    public void hacerSonido() {
        System.out.println("El animal hace un sonido");
    }
}

public class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("El perro ladra");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal miAnimal = new Animal();
        Animal miPerro = new Perro();

        miAnimal.hacerSonido(); // Imprime: El animal hace un sonido
        miPerro.hacerSonido(); // Imprime: El perro ladra
    }
}
```
### Conclusión

La herencia y el polimorfismo son conceptos clave en Java que permiten reutilizar código y crear sistemas más flexibles y mantenibles. La herencia permite que las clases compartan un conjunto común de comportamientos y propiedades, mientras que el polimorfismo permite que el mismo código trabaje con diferentes tipos de objetos de manera transparente.

### Consideraciones Adicionales

- **Diseño de Clases:** Usa la herencia con cuidado. Demasiada herencia puede llevar a una jerarquía de clases complicada y difícil de mantener.
- **Interfaz vs. Herencia:** Considera el uso de interfaces y composición en lugar de herencia en algunos casos, ya que puede proporcionar mayor flexibilidad.
- **Sobreescritura de Métodos:** Al sobrescribir métodos, usa la anotación `@Override` para asegurar que estás realmente sobrescribiendo un método en la superclase.
- **Principio de Sustitución de Liskov:** Asegúrate de que las subclases puedan ser usadas en lugar de la superclase sin alterar el comportamiento esperado del programa.

