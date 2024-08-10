### Implementar Localización Usando Locales, Resource Bundles, Parseo y Formateo de Mensajes, Fechas, Horas, Números, Incluyendo Valores de Moneda y Porcentajes

La localización (i18n) en Java es el proceso de adaptar una aplicación para diferentes idiomas y regiones sin modificar el código fuente. Esto implica el uso de clases y métodos que permiten manejar diferentes `Locales`, `Resource Bundles`, y el parseo y formateo de mensajes, fechas, horas, y números, incluyendo valores de moneda y porcentajes.

### 1. Locales

Un `Locale` representa una región geográfica o cultural. En Java, se puede usar la clase `Locale` para manejar información específica de un país o idioma, como formatos de fecha, hora, números, y más.

**Ejemplo:**

```java
import java.util.Locale;

public class EjemploLocale {
    public static void main(String[] args) {
        // Crear un Locale para Estados Unidos
        Locale localeUS = Locale.US;
        
        // Crear un Locale para Francia
        Locale localeFR = Locale.FRANCE;
        
        // Crear un Locale para un idioma específico
        Locale localeES = new Locale("es", "ES");
        
        System.out.println("Locale de Estados Unidos: " + localeUS);
        System.out.println("Locale de Francia: " + localeFR);
        System.out.println("Locale de España: " + localeES);
    }
}
```

### 2. Resource Bundles

Los `Resource Bundles` se utilizan para almacenar textos y otros recursos que pueden variar según el `Locale`. Esto permite cambiar fácilmente los textos de la interfaz de usuario en función del idioma o región.

**Ejemplo:**

1. **Archivo `MessagesBundle_en_US.properties`**:
   ```properties
   saludo=Hello
   ```

2. **Archivo `MessagesBundle_es_ES.properties`**:
   ```properties
   saludo=Hola
   ```

3. **Código Java para cargar un `ResourceBundle`:**
   ```java
   import java.util.Locale;
   import java.util.ResourceBundle;

   public class EjemploResourceBundle {
       public static void main(String[] args) {
           Locale localeES = new Locale("es", "ES");
           Locale localeUS = Locale.US;

           ResourceBundle bundleES = ResourceBundle.getBundle("MessagesBundle", localeES);
           ResourceBundle bundleUS = ResourceBundle.getBundle("MessagesBundle", localeUS);

           System.out.println("Saludo en español: " + bundleES.getString("saludo"));
           System.out.println("Saludo en inglés: " + bundleUS.getString("saludo"));
       }
   }
   ```

### 3. Parseo y Formateo de Mensajes

El parseo y formateo de mensajes permite personalizar la salida de cadenas en función del `Locale`.

**Ejemplo:**

```java
import java.text.MessageFormat;
import java.util.Locale;
import java.util.ResourceBundle;

public class EjemploFormatoMensaje {
    public static void main(String[] args) {
        Locale localeES = new Locale("es", "ES");
        ResourceBundle bundle = ResourceBundle.getBundle("MessagesBundle", localeES);

        String patron = bundle.getString("saludo");
        String mensaje = MessageFormat.format(patron, "Carlos");
        System.out.println(mensaje);
    }
}
```

**Archivo `MessagesBundle_es_ES.properties`**:
```properties
saludo=Hola {0}, bienvenido.
```

### 4. Formateo de Fechas y Horas

El formateo de fechas y horas depende del `Locale` para mostrar la información de manera correcta según la región.

**Ejemplo:**

```java
import java.text.DateFormat;
import java.util.Date;
import java.util.Locale;

public class EjemploFormatoFecha {
    public static void main(String[] args) {
        Locale localeFR = Locale.FRANCE;
        Locale localeUS = Locale.US;
        Date ahora = new Date();

        DateFormat formatoFR = DateFormat.getDateInstance(DateFormat.FULL, localeFR);
        DateFormat formatoUS = DateFormat.getDateInstance(DateFormat.FULL, localeUS);

        System.out.println("Fecha en Francia: " + formatoFR.format(ahora));
        System.out.println("Fecha en Estados Unidos: " + formatoUS.format(ahora));
    }
}
```

### 5. Formateo de Números, Moneda y Porcentajes

El formateo de números, incluyendo moneda y porcentajes, también depende del `Locale`.

**Ejemplo:**

```java
import java.text.NumberFormat;
import java.util.Locale;

public class EjemploFormatoNumero {
    public static void main(String[] args) {
        double numero = 12345.67;

        NumberFormat formatoNumero = NumberFormat.getNumberInstance(Locale.GERMANY);
        NumberFormat formatoMoneda = NumberFormat.getCurrencyInstance(Locale.US);
        NumberFormat formatoPorcentaje = NumberFormat.getPercentInstance(Locale.FRANCE);

        System.out.println("Número (Alemania): " + formatoNumero.format(numero));
        System.out.println("Moneda (Estados Unidos): " + formatoMoneda.format(numero));
        System.out.println("Porcentaje (Francia): " + formatoPorcentaje.format(0.85));
    }
}
```

### Conclusión y Consideraciones Adicionales

La localización en Java permite a las aplicaciones adaptarse fácilmente a diferentes idiomas y regiones, mejorando la experiencia del usuario. Comprender cómo usar `Locale`, `Resource Bundles`, y las clases de formateo para fechas, horas, números, y textos es esencial para desarrollar aplicaciones globalizadas. Es fundamental familiarizarse con estas herramientas y técnicas para manejar de manera efectiva la variabilidad cultural y lingüística en aplicaciones Java.