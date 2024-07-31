## Modificadores de Acceso (public, private, protected, default)

### 1. Modificadores de Acceso

En Java, los modificadores de acceso controlan la visibilidad de clases, métodos y variables. Los cuatro niveles de acceso son `public`, `protected`, `default` (sin modificador explícito), y `private`.

### 2. `public`

El modificador `public` hace que un miembro de la clase sea accesible desde cualquier otra clase.

**Ejemplo:**
```java
public class Persona {
    public String nombre;
    public int edad;

    public void mostrarInformacion() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }
}
```
**Acceso desde otra clase:**
```java
public class Main {
    public static void main(String[] args) {
        Persona persona = new Persona();
        persona.nombre = "Juan";
        persona.edad = 30;
        persona.mostrarInformacion(); // Imprime: Nombre: Juan, Edad: 30
    }
}
```
### 3. `private`

El modificador `private` hace que un miembro de la clase sea accesible solo dentro de la misma clase. No puede ser accedido desde ninguna otra clase, incluyendo subclases.

**Ejemplo:**
```java
public class Persona {
    private String nombre;
    private int edad;

    private void mostrarInformacion() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }
}
```
**Acceso desde otra clase:**
```java
public class Main {
    public static void main(String[] args) {
        Persona persona = new Persona();
        persona.setNombre("Juan");
        persona.setEdad(30);
        // persona.nombre y persona.edad no son accesibles directamente
    }
}
```
### 4. `protected`

El modificador `protected` permite que un miembro de la clase sea accesible dentro de su propio paquete y por subclases.

**Ejemplo:**
```java
public class Persona {
    protected String nombre;
    protected int edad;

    protected void mostrarInformacion() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }
}
```
**Acceso desde una subclase en el mismo paquete:**
```java
public class Empleado extends Persona {
    public void mostrar() {
        nombre = "Ana";
        edad = 25;
        mostrarInformacion(); // Imprime: Nombre: Ana, Edad: 25
    }
}
```
### 5. `default` (sin modificador)

El acceso `default` hace que un miembro de la clase sea accesible solo dentro del mismo paquete. Si no se especifica ningún modificador de acceso, se aplica el acceso `default`.

**Ejemplo:**
```java
public class Persona {
    String nombre;
    int edad;

    void mostrarInformacion() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }
}
```
**Acceso desde otra clase en el mismo paquete:**
```java
public class Main {
    public static void main(String[] args) {
        Persona persona = new Persona();
        persona.nombre = "Juan";
        persona.edad = 30;
        persona.mostrarInformacion(); // Imprime: Nombre: Juan, Edad: 30
    }
}
```
### Conclusión

Los modificadores de acceso en Java proporcionan un mecanismo para controlar la visibilidad y accesibilidad de los miembros de una clase. El uso adecuado de estos modificadores ayuda a proteger la integridad de los datos y a diseñar clases bien encapsuladas.

### Consideraciones Adicionales

- **Encapsulación:** Utiliza `private` para los campos de clase y proporciona métodos públicos para acceder y modificar estos campos (getters y setters).
- **Herencia:** Usa `protected` para miembros que deben ser accesibles en subclases pero no en otras clases.
- **Paquete:** Aprovecha el acceso `default` para restringir el acceso a miembros solo dentro del mismo paquete.
- **API Pública:** Utiliza `public` con precaución para miembros que deben ser accesibles desde cualquier lugar.
