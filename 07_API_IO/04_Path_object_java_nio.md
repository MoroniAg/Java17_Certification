### Crear, recorrer, leer y escribir objetos `Path` y sus propiedades utilizando la API `java.nio.file`

El paquete `java.nio.file` introducido en Java 7 proporciona una API moderna y robusta para trabajar con archivos y directorios. La clase `Path` es central en esta API, permitiendo representar rutas de archivos de una manera más flexible y poderosa que la clase `File` de las versiones anteriores de Java.

### 1. Crear objetos `Path`

El objeto `Path` representa una ruta a un archivo o directorio en el sistema de archivos. Se puede crear utilizando la clase `Paths` o mediante el método `File.toPath()`.

**Ejemplo:**

```java
import java.nio.file.Path;
import java.nio.file.Paths;

public class CrearPath {
    public static void main(String[] args) {
        // Crear un Path desde una cadena de texto
        Path path = Paths.get("C:/ejemplo/archivo.txt");

        // Crear un Path usando un array de strings
        Path path2 = Paths.get("C:", "ejemplo", "archivo.txt");

        System.out.println("Path 1: " + path);
        System.out.println("Path 2: " + path2);
    }
}
```

### 2. Recorrer un objeto `Path`

Un objeto `Path` puede ser recorrido para acceder a sus distintos elementos, como nombres de directorios y el nombre del archivo.

**Ejemplo:**

```java
public class RecorrerPath {
    public static void main(String[] args) {
        Path path = Paths.get("C:/ejemplo/archivo.txt");

        // Recorrer cada elemento del Path
        for (int i = 0; i < path.getNameCount(); i++) {
            System.out.println("Elemento " + i + ": " + path.getName(i));
        }
    }
}
```

### 3. Leer propiedades de un objeto `Path`

La clase `Path` permite acceder a varias propiedades, como el nombre del archivo, el nombre de la raíz, el directorio principal, etc.

**Ejemplo:**

```java
public class LeerPropiedadesPath {
    public static void main(String[] args) {
        Path path = Paths.get("C:/ejemplo/archivo.txt");

        System.out.println("Nombre del archivo: " + path.getFileName());
        System.out.println("Ruta absoluta: " + path.toAbsolutePath());
        System.out.println("Nombre de la raíz: " + path.getRoot());
        System.out.println("Nombre del directorio padre: " + path.getParent());
    }
}
```

### 4. Escribir y leer archivos utilizando la API `java.nio.file`

La API `java.nio.file.Files` proporciona métodos para leer y escribir archivos de manera sencilla y eficiente.

#### Escribir un archivo

**Ejemplo:**

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;

public class EscribirArchivo {
    public static void main(String[] args) {
        Path path = Paths.get("C:/ejemplo/archivo.txt");
        String contenido = "Este es un ejemplo de escritura en un archivo usando java.nio.file.";

        try {
            Files.write(path, contenido.getBytes());
            System.out.println("Archivo escrito con éxito.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### Leer un archivo

**Ejemplo:**

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;

public class LeerArchivo {
    public static void main(String[] args) {
        Path path = Paths.get("C:/ejemplo/archivo.txt");

        try {
            String contenido = Files.readString(path);
            System.out.println("Contenido del archivo: \n" + contenido);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 5. Recorrer directorios y manejar archivos

La API `java.nio.file` facilita la tarea de recorrer directorios y realizar operaciones en archivos.

**Ejemplo:**

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;

public class RecorrerDirectorios {
    public static void main(String[] args) {
        Path dir = Paths.get("C:/ejemplo");

        try {
            Files.list(dir).forEach(path -> {
                if (Files.isDirectory(path)) {
                    System.out.println("Directorio: " + path.getFileName());
                } else {
                    System.out.println("Archivo: " + path.getFileName());
                }
            });
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Conclusión y Consideraciones Adicionales

La API `java.nio.file` es una herramienta poderosa para trabajar con archivos y directorios en Java. Ofrece una mayor flexibilidad, robustez y eficiencia en comparación con las antiguas clases de manejo de archivos. Al prepararte para la certificación, es esencial familiarizarse con estas herramientas y comprender las diversas operaciones que pueden realizarse con objetos `Path`. Asegúrate de practicar la creación, manipulación y lectura de rutas y archivos para dominar estas técnicas en diferentes escenarios.