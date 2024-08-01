### Implementar Herencia, Clases Abstractas y Selladas, Sobrescribir Métodos, Implementar Polimorfismo y Diferenciar Tipo de Objeto vs Tipo de Referencia

#### Herencia

La herencia es un principio fundamental en la programación orientada a objetos que permite que una clase (subclase) herede propiedades y métodos de otra clase (superclase). En Java, esto se logra utilizando la palabra clave `extends`.

*Ejemplo:*

```java
public class Animal {
    public void hacerSonido() {
        System.out.println("Sonido de animal");
    }
}

public class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Ladrido");
    }
}
```

#### Clases Abstractas

Las clases abstractas no pueden ser instanciadas directamente y pueden contener métodos abstractos (sin implementación). Se utilizan para definir una estructura base que otras clases pueden extender.

*Ejemplo:*

```java
public abstract class Animal {
    public abstract void hacerSonido();

    public void dormir() {
        System.out.println("El animal está durmiendo");
    }
}

public class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Ladrido");
    }
}
```

Las clases abstractas en Java son clases que no se pueden instanciar directamente y se utilizan para proporcionar una base común que otras clases pueden extender. Las clases abstractas pueden contener métodos abstractos y métodos concretos. Un método abstracto es aquel que no tiene implementación en la clase abstracta y debe ser implementado por las subclases.

**Características de las clases abstractas:**
- No pueden ser instanciadas directamente.
- Pueden contener métodos abstractos y métodos concretos.
- Pueden tener variables de instancia.
- Pueden tener constructores, que pueden ser llamados por las subclases.

**Ejemplo de clase abstracta:**

```java
public abstract class Animal {
    private String nombre;

    public Animal(String nombre) {
        this.nombre = nombre;
    }

    public String getNombre() {
        return nombre;
    }

    // Método abstracto
    public abstract void hacerSonido();

    // Método concreto
    public void dormir() {
        System.out.println(nombre + " está durmiendo");
    }
}

public class Perro extends Animal {
    public Perro(String nombre) {
        super(nombre);
    }

    @Override
    public void hacerSonido() {
        System.out.println("Ladrido");
    }
}

public class Gato extends Animal {
    public Gato(String nombre) {
        super(nombre);
    }

    @Override
    public void hacerSonido() {
        System.out.println("Maullido");
    }
}
```

En este ejemplo, `Animal` es una clase abstracta con un método abstracto `hacerSonido()` y un método concreto `dormir()`. Las clases `Perro` y `Gato` extienden `Animal` y proporcionan implementaciones específicas para `hacerSonido()`.


#### Clases Selladas

Introducidas en Java 17, las clases selladas restringen qué otras clases pueden extenderlas. Se declaran usando la palabra clave `sealed` y sus subclases deben ser explícitamente permitidas usando `permits`.

*Ejemplo:*

```java
public sealed class Animal permits Perro, Gato {
}

public final class Perro extends Animal {
}

public final class Gato extends Animal {
}
```

#### Sobrescribir Métodos

Sobrescribir métodos es una característica que permite a una subclase proporcionar una implementación específica de un método que ya está definido en su superclase.

*Ejemplo:*

```java
public class Animal {
    public void hacerSonido() {
        System.out.println("Sonido de animal");
    }
}

public class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Ladrido");
    }
}
```

Sobrescribir métodos de la clase `Object` como `toString`, `equals`, y `hashCode` es común para personalizar la representación y comparación de objetos.

*Ejemplo:*

```java
public class Persona {
    private String nombre;
    private int edad;

    @Override
    public String toString() {
        return "Persona{nombre='" + nombre + "', edad=" + edad + "}";
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Persona persona = (Persona) o;
        return edad == persona.edad && nombre.equals(persona.nombre);
    }

    @Override
    public int hashCode() {
        return Objects.hash(nombre, edad);
    }
}
```


#### Polimorfismo

El polimorfismo es un principio fundamental de la programación orientada a objetos que permite que las clases relacionadas por herencia sean tratadas de manera uniforme. En Java, el polimorfismo se manifiesta principalmente en dos formas: el polimorfismo de inclusión (subtipo) y el polimorfismo paramétrico (generics).

**Polimorfismo de inclusión:**
Permite que una referencia de superclase apunte a objetos de cualquier subclase. Esto es posible gracias a la herencia y a la sobrescritura de métodos.

**Ejemplo:**

```java
public class Main {
    public static void main(String[] args) {
        Animal miAnimal = new Perro("Fido");
        miAnimal.hacerSonido();  // Llamará al método hacerSonido() de Perro

        miAnimal = new Gato("Mishi");
        miAnimal.hacerSonido();  // Llamará al método hacerSonido() de Gato
    }
}
```

En este ejemplo, la variable `miAnimal` de tipo `Animal` puede referirse a objetos de tipo `Perro` y `Gato`. La llamada a `hacerSonido()` se resuelve en tiempo de ejecución al método específico de la subclase.

**Polimorfismo paramétrico (Generics):**
Permite definir métodos, clases e interfaces con parámetros de tipo, lo que proporciona un mayor nivel de abstracción y reutilización de código.

**Ejemplo:**

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Animal> animales = new ArrayList<>();
        animales.add(new Perro("Fido"));
        animales.add(new Gato("Mishi"));

        for (Animal animal : animales) {
            animal.hacerSonido();  // Llamará al método hacerSonido() de cada objeto específico
        }
    }
}
```

En este ejemplo, la lista `animales` puede contener objetos de cualquier subclase de `Animal`. El uso de generics permite que la lista sea tipada, proporcionando seguridad en tiempo de compilación.


#### Diferenciar Tipo de Objeto vs Tipo de Referencia

El tipo de referencia de una variable es el tipo declarado en la variable, mientras que el tipo de objeto es el tipo real del objeto al que la variable se refiere.

*Ejemplo:*

```java
Animal animal = new Perro(); // Tipo de referencia: Animal, Tipo de objeto: Perro
```

#### Casting de Tipos

El casting de tipos permite convertir un tipo de referencia a otro. Existen dos tipos de casting: explícito e implícito.

*Ejemplo de casting explícito:*

```java
Animal animal = new Perro();
Perro perro = (Perro) animal; // Casting explícito de Animal a Perro
```

#### Operador `instanceof` y Emparejamiento de Patrones

El operador `instanceof` verifica si un objeto es una instancia de una clase específica.

*Ejemplo:*

```java
if (animal instanceof Perro) {
    Perro perro = (Perro) animal;
    perro.hacerSonido();
}
```

Java 16 introdujo el emparejamiento de patrones para `instanceof`, simplificando el código.

*Ejemplo:*

```java
if (animal instanceof Perro perro) {
    perro.hacerSonido();
}
```

### Conclusión y Consideraciones Adicionales

La herencia y el polimorfismo son conceptos esenciales en la programación orientada a objetos que permiten reutilizar y extender el código de manera eficiente. La sobrescritura de métodos y el uso adecuado de las clases abstractas y selladas ayudan a definir comportamientos específicos y restringir el diseño del sistema. Entender y utilizar correctamente el casting de tipos, el operador `instanceof` y el emparejamiento de patrones es crucial para manipular y verificar tipos de manera segura y efectiva en Java.

Las clases abstractas y el polimorfismo son conceptos esenciales en la programación orientada a objetos que facilitan la creación de jerarquías de clases y la reutilización de código. Las clases abstractas permiten definir una estructura común y dejar detalles específicos a las subclases. El polimorfismo, tanto de inclusión como paramétrico, proporciona flexibilidad al permitir que el código trabaje con objetos de diferentes tipos de manera uniforme.

Comprender y utilizar adecuadamente estos conceptos es crucial para diseñar sistemas de software robustos y mantenibles. Asegúrese de practicar la implementación y el uso de clases abstractas y polimorfismo para consolidar estos conocimientos.

### Referencias

Oracle. (2023). Java Platform, Standard Edition 17 API Specification. Retrieved from [https://docs.oracle.com/en/java/javase/17/docs/api/index.html](https://docs.oracle.com/en/java/javase/17/docs/api/index.html).
