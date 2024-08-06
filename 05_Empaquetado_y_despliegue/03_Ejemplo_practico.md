Claro, te proporcionaré un ejemplo paso a paso, detallado y descriptivo, sobre cómo compilar un código Java, crear un archivo JAR modular y luego crear una imagen de tiempo de ejecución utilizando los comandos `javac`, `jar` y `jlink`.

### Paso 1: Estructura del Proyecto

Supongamos que tienes un proyecto con la siguiente estructura:

```
/mi-proyecto
    /src
        /com
            /ejemplo
                Main.java
                Util.java
    /mods
    /mlib
```

### Paso 2: Código de Ejemplo

#### `Main.java`

```java
package com.ejemplo;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hola, Mundo!");
        Util.saludar("Carlos");
    }
}
```

#### `Util.java`

```java
package com.ejemplo;

public class Util {
    public static void saludar(String nombre) {
        System.out.println("Hola, " + nombre);
    }
}
```

### Paso 3: Compilación del Código

Usaremos el comando `javac` para compilar el código fuente y colocar los archivos `.class` en el directorio `mods`.

```bash
javac -d mods/com.ejemplo $(find src -name "*.java")
```

- `-d mods/com.ejemplo`: Especifica que los archivos compilados deben colocarse en `mods/com.ejemplo`.
- `$(find src -name "*.java")`: Encuentra todos los archivos `.java` en el directorio `src` y sus subdirectorios.

### Paso 4: Crear el Archivo JAR Modular

Usaremos el comando `jar` para crear un archivo JAR modular del proyecto compilado.

```bash
jar --create --file=mlib/com.ejemplo.jar --module-version=1.0 -C mods/com.ejemplo .
```

- `--create`: Indica que se va a crear un nuevo archivo JAR.
- `--file=mlib/com.ejemplo.jar`: Especifica el nombre y ubicación del archivo JAR.
- `--module-version=1.0`: Establece la versión del módulo.
- `-C mods/com.ejemplo .`: Cambia al directorio `mods/com.ejemplo` y añade todos sus archivos al JAR.

### Paso 5: Ejecutar el Archivo JAR Modular

Para ejecutar el archivo JAR modular, utilizamos el comando `java` con la opción `--module`.

```bash
java --module-path mlib --module com.ejemplo/com.ejemplo.Main
```

- `--module-path mlib`: Especifica el directorio que contiene los módulos (en este caso, `mlib`).
- `--module com.ejemplo/com.ejemplo.Main`: Especifica el módulo y la clase principal a ejecutar.

### Paso 6: Crear una Imagen de Tiempo de Ejecución

Finalmente, usaremos `jlink` para crear una imagen de tiempo de ejecución que incluya el módulo `com.ejemplo`.

```bash
jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.ejemplo --output miimagen
```

- `--module-path $JAVA_HOME/jmods:mlib`: Especifica los caminos a los módulos necesarios (`$JAVA_HOME/jmods` para los módulos estándar de Java y `mlib` para el módulo personalizado).
- `--add-modules com.ejemplo`: Añade el módulo `com.ejemplo` a la imagen de tiempo de ejecución.
- `--output miimagen`: Especifica el directorio donde se creará la imagen de tiempo de ejecución.

### Paso 7: Ejecutar la Imagen de Tiempo de Ejecución

Para ejecutar la imagen de tiempo de ejecución creada, navega al directorio `miimagen/bin` y ejecuta el archivo `java` con el módulo y clase principal.

```bash
cd miimagen/bin
./java --module com.ejemplo/com.ejemplo.Main
```

### Resumen de Comandos Utilizados

1. Compilación:
    ```bash
    javac -d mods/com.ejemplo $(find src -name "*.java")
    ```

2. Creación del JAR Modular:
    ```bash
    jar --create --file=mlib/com.ejemplo.jar --module-version=1.0 -C mods/com.ejemplo .
    ```

3. Ejecución del JAR Modular:
    ```bash
    java --module-path mlib --module com.ejemplo/com.ejemplo.Main
    ```

4. Creación de Imagen de Tiempo de Ejecución:
    ```bash
    jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.ejemplo --output miimagen
    ```

5. Ejecución de la Imagen de Tiempo de Ejecución:
    ```bash
    cd miimagen/bin
    ./java --module com.ejemplo/com.ejemplo.Main
    ```

### Conclusión y Consideraciones Adicionales

Este proceso te permite compilar, empaquetar y ejecutar aplicaciones Java de manera modular. Entender estos comandos y sus opciones te preparará mejor para manejar proyectos Java complejos y optimizar el rendimiento y la seguridad de tus aplicaciones. Practica con estos comandos y adapta los ejemplos a tus necesidades específicas para dominar estas herramientas.

Si tienes alguna otra duda o necesitas más detalles sobre algún paso en particular, ¡házmelo saber!