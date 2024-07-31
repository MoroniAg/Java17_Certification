### Manipulación de Texto en Java: Bloques de Texto y Clases `String` y `StringBuilder`

#### Manipulación de Texto

En Java, la manipulación de texto se realiza principalmente utilizando las clases `String` y `StringBuilder`. Estas clases ofrecen métodos para crear, modificar y analizar cadenas de texto.

#### 1. Clase `String`

La clase `String` en Java representa una secuencia de caracteres y es inmutable. Esto significa que una vez que se crea una instancia de `String`, su valor no puede ser modificado.

**1.1 Creación de Cadenas**

Las cadenas de texto se pueden crear de dos maneras:

```java
String saludo = "Hola, mundo!";
String saludo2 = new String("Hola, mundo!");
```

**1.2 Métodos Comunes**

- `length()`: Devuelve la longitud de la cadena.

  ```java
  String texto = "Java";
  int longitud = texto.length(); // Resultado: 4
  ```

- `charAt(int index)`: Devuelve el carácter en la posición especificada.

  ```java
  char letra = texto.charAt(2); // Resultado: 'v'
  ```

- `substring(int beginIndex, int endIndex)`: Devuelve una subcadena desde el índice `beginIndex` hasta `endIndex`.

  ```java
  String subcadena = texto.substring(1, 3); // Resultado: "av"
  ```

- `toUpperCase()`: Convierte todos los caracteres de la cadena a mayúsculas.

  ```java
  String mayusculas = texto.toUpperCase(); // Resultado: "JAVA"
  ```

- `toLowerCase()`: Convierte todos los caracteres de la cadena a minúsculas.

  ```java
  String minusculas = texto.toLowerCase(); // Resultado: "java"
  ```

- `trim()`: Elimina los espacios en blanco al inicio y al final de la cadena.

  ```java
  String textoConEspacios = "  Java  ";
  String textoLimpio = textoConEspacios.trim(); // Resultado: "Java"
  ```

- `replace(CharSequence target, CharSequence replacement)`: Reemplaza todas las ocurrencias de `target` con `replacement`.

  ```java
  String reemplazo = texto.replace("Java", "JavaScript"); // Resultado: "JavaScript"
  ```

- `concat(String str)`: Concatena la cadena especificada al final de esta cadena.

  ```java
  String concatenado = texto.concat(" Programming"); // Resultado: "Java Programming"
  ```

**1.3 Ejemplo Avanzado**

```java
String mensaje = "  Bienvenido a Java!  ";
String mensajeLimpio = mensaje.trim().toLowerCase();
String mensajeReemplazado = mensajeLimpio.replace("java", "programación en Java");
```

**Resultado:**
- `mensajeLimpio`: `"bienvenido a java!"`
- `mensajeReemplazado`: `"bienvenido a programación en Java!"`

#### 2. Clase `StringBuilder`

La clase `StringBuilder` es mutable y se utiliza para construir cadenas de texto que cambian frecuentemente. Permite modificar el contenido sin crear nuevas instancias de cadena.

**2.1 Creación de `StringBuilder`**

```java
StringBuilder sb = new StringBuilder("Hola");
sb.append(", mundo!");
```

**2.2 Métodos Comunes**

- `append(String str)`: Añade la cadena especificada al final del `StringBuilder`.

  ```java
  sb.append(" - ¡Hola Mundo!"); // Resultado: "Hola, mundo! - ¡Hola Mundo!"
  ```

- `insert(int offset, String str)`: Inserta la cadena especificada en la posición indicada.

  ```java
  sb.insert(5, " querido"); // Resultado: "Hola querido, mundo! - ¡Hola Mundo!"
  ```

- `delete(int start, int end)`: Elimina el texto entre los índices `start` y `end`.

  ```java
  sb.delete(5, 13); // Resultado: "Hola, mundo! - ¡Hola Mundo!"
  ```

- `reverse()`: Invierte el contenido del `StringBuilder`.

  ```java
  sb.reverse(); // Resultado: "!odnuH aloH - !odnuoc ,aloH"
  ```

- `toString()`: Convierte el `StringBuilder` a una cadena `String`.

  ```java
  String resultado = sb.toString(); // Resultado: "!odnuH aloH - !odnuoc ,aloH"
  ```

**2.3 Ejemplo Avanzado**

```java
StringBuilder sb = new StringBuilder("Texto inicial");
sb.append(" modificado");
sb.insert(11, " - ");
sb.reverse();
String resultado = sb.toString();
```

**Resultado:**
- `resultado`: `"odificado - txeT"`

#### 3. Bloques de Texto

Los bloques de texto (introducidos en Java 13) permiten manejar cadenas multilínea con formato sin necesidad de concatenar cadenas o usar secuencias de escape.

**3.1 Creación de Bloques de Texto**

```java
String bloqueDeTexto = """
    Este es un bloque de texto.
    Puede contener varias líneas.
    Los espacios y saltos de línea se mantienen.
    """;
```

**3.2 Métodos para Manipular Bloques de Texto**

Los bloques de texto se comportan como cadenas `String`, así que puedes usar los métodos de `String` para manipularlos.

**Ejemplo 1:**

```java
String bloqueDeTexto = """
    Línea 1
    Línea 2
    Línea 3
    """;
String[] lineas = bloqueDeTexto.split("\n");
for (String linea : lineas) {
    System.out.println(linea);
}
```

**Ejemplo 2:**

```java
String bloqueDeTexto = """
    Este es un bloque de texto.
    Aquí hay varias líneas.
    """;
String textoLimpiado = bloqueDeTexto.trim(); // Elimina espacios en blanco al principio y al final
```

### Conclusión y Consideraciones Adicionales

Comprender cómo manipular texto utilizando `String`, `StringBuilder` y bloques de texto es fundamental en Java. La clase `String` es ideal para operaciones que no requieren modificaciones frecuentes, mientras que `StringBuilder` ofrece una manera eficiente de construir y modificar cadenas de texto. Los bloques de texto, por su parte, simplifican el manejo de cadenas multilínea, manteniendo su formato y mejorando la legibilidad. Estos conceptos son clave para el manejo efectivo de datos textuales en Java y son relevantes para la certificación de Java 17.