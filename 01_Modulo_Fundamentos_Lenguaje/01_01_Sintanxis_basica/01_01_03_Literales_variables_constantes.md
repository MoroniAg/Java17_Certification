## Literales, Variables y Constantes

### Literales

Los literales en Java representan valores constantes que se utilizan directamente en el código. Aquí se detallan los diferentes tipos de literales:

**1. Literales Enteros**

Representan valores enteros y pueden ser expresados en diferentes bases:

- **Decimal:** Base 10 (por defecto)

  ```java
  int edad = 25; // Valor decimal
  ```

- **Octal:** Base 8 (precedido por `0`)

  ```java
  int octal = 017; // 15 en decimal
  ```

- **Hexadecimal:** Base 16 (precedido por `0x` o `0X`)

  ```java
  int hexadecimal = 0x1A; // 26 en decimal
  ```

**2. Literales de Punto Flotante**

Representan valores decimales y pueden ser de precisión simple (`float`) o doble (`double`).

- **Decimal (double por defecto):**

  ```java
  double pi = 3.14159;
  ```

- **Decimal (float, seguido por `f` o `F`):**

  ```java
  float temperatura = 36.6f; // Valor de precisión simple
  ```

**3. Literales de Carácter**

Representan un solo carácter Unicode, encerrado entre comillas simples.

```java
char letra = 'A'; // Valor de carácter
```

**4. Literales de Cadena**

Representan una secuencia de caracteres, encerrada entre comillas dobles.

```java
String mensaje = "Bienvenido a Java 17";
```

**5. Literales Booleanos**

Representan valores lógicos, `true` o `false`.

```java
boolean esActivo = true;
```

**6. Literales Null**

Representan la ausencia de un valor y se utilizan para variables de referencia.

```java
String texto = null; // No apunta a ningún objeto
```

### Variables

Las variables en Java se utilizan para almacenar datos. Deben ser declaradas antes de usarlas y pueden ser inicializadas con valores.

**Declaración e Inicialización de Variables**

```java
int edad = 30; // Declaración e inicialización
```

**Tipos de Variables**

- **Variables Locales:** Declaradas dentro de métodos, bloques o constructores. Solo accesibles dentro de su ámbito.

  ```java
  public void calcularArea() {
      int radio = 5; // Variable local
      double area = Math.PI * radio * radio;
      System.out.println("Área: " + area);
  }
  ```

- **Variables de Instancia:** Declaradas en una clase fuera de cualquier método. Accesibles a todas las instancias de la clase.

  ```java
  public class Coche {
      String modelo; // Variable de instancia

      public Coche(String modelo) {
          this.modelo = modelo;
      }
  }
  ```

- **Variables de Clase (Estáticas):** Declaradas con la palabra clave `static`. Compartidas por todas las instancias de la clase.

  ```java
  public class Contador {
      static int conteo = 0; // Variable de clase

      public void incrementar() {
          conteo++;
      }
  }
  ```

**Reglas para Nombrar Variables**

- Deben comenzar con una letra, `$`, o `_`.
- Los nombres deben ser únicos dentro de su ámbito.
- Se recomienda usar camelCase para los nombres de variables.

### Constantes

Las constantes en Java son valores que no cambian una vez asignados. Se definen utilizando la palabra clave `final`.

**Declaración de Constantes**

- Las constantes se declaran con `final` y suelen ser `static` para compartirlas entre instancias.

  ```java
  public class Constantes {
      public static final int MAX_EDAD = 100; // Constante de clase
  }
  ```

- Las constantes se escriben en mayúsculas por convención, y los nombres se separan con guiones bajos.

**Uso de Constantes**

Las constantes se utilizan en el código para representar valores fijos. Al ser `static`, se pueden acceder a través de la clase.

```java
public class PruebaConstantes {
    public static void main(String[] args) {
        System.out.println("Edad máxima permitida: " + Constantes.MAX_EDAD);
    }
}
```

### Ejemplo Completo

```java
public class Calculadora {

    public static final double PI = 3.14159; // Constante de clase

    public static void main(String[] args) {
        int radio = 7; // Variable local
        double area = PI * radio * radio; // Uso de constante y variable
        System.out.println("Área del círculo: " + area);
        
        String mensaje = "El cálculo se realizó correctamente"; // Literal de cadena
        System.out.println(mensaje);
    }
}
```

### Conclusión

Los literales, variables y constantes son conceptos fundamentales en Java. Los literales permiten representar valores constantes en el código, mientras que las variables permiten almacenar y manipular datos. Las constantes, al ser inmutables, proporcionan un medio para definir valores que no cambian a lo largo del tiempo, mejorando la legibilidad y mantenimiento del código.

### Consideraciones Adicionales

- **Inicialización de Variables:** Asegúrate de inicializar las variables antes de su uso para evitar errores en tiempo de ejecución.
- **Uso de Constantes:** Utiliza constantes para valores que no cambian para evitar errores y mejorar la claridad del código.
- **Tipos de Literales:** Elige el tipo de literal adecuado para el contexto y asegúrate de usar sufijos correctos (`f` para `float`, `L` para `long`) para evitar errores de tipo.
