### Compilación de Código Java, Producción de JARs Modulares y No Modulares, Imágenes de Tiempo de Ejecución e Implementación de Migración con Módulos No Nombrados y Automáticos

#### Compilación de Código Java

La compilación de código Java es el proceso de convertir el código fuente escrito en archivos `.java` a bytecode que la Máquina Virtual Java (JVM) puede ejecutar. Esto se realiza utilizando el compilador `javac`.

##### Ejemplo de Compilación

```bash
javac com/ejemplo/Main.java
```

Esto genera un archivo `Main.class` que contiene el bytecode de la clase `Main`.

#### Producción de JARs Modulares y No Modulares

##### JARs No Modulares

Un archivo JAR (Java ARchive) no modular es un contenedor que agrupa varios archivos `.class` y otros recursos (como archivos de propiedades e imágenes) en un solo archivo.

###### Creación de un JAR No Modular

```bash
jar cf ejemplo.jar -C ruta/al/directorio/clases .
```

Este comando crea un archivo JAR llamado `ejemplo.jar` a partir del contenido del directorio especificado.

##### JARs Modulares

Un JAR modular contiene un archivo `module-info.class` en su raíz, que define el módulo y sus dependencias.

###### Creación de un JAR Modular

Primero, compila el código fuente incluyendo el descriptor del módulo:

```bash
javac -d mods/com.ejemplo $(find src -name "*.java")
```

Luego, crea el archivo JAR modular:

```bash
jar --create --file=mlib/com.ejemplo.jar --module-version=1.0 -C mods/com.ejemplo .
```

#### Producción de Imágenes de Tiempo de Ejecución

Una imagen de tiempo de ejecución es una distribución personalizada de la JVM, el módulo de la aplicación y sus dependencias, que permite ejecutar la aplicación sin necesidad de una instalación separada de la JVM.

##### Creación de una Imagen de Tiempo de Ejecución

Usa la herramienta `jlink` para crear una imagen de tiempo de ejecución:

```bash
jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.ejemplo --output miimagen
```

Este comando crea una imagen de tiempo de ejecución en el directorio `miimagen`, incluyendo el módulo `com.ejemplo` y sus dependencias.

#### Implementación de Migración con Módulos No Nombrados y Automáticos

##### Módulos No Nombrados

Los módulos no nombrados permiten utilizar bibliotecas de terceros que no están modularizadas. Se colocan en el classpath en lugar del modulepath.

###### Ejemplo de Uso de Módulos No Nombrados

```bash
java -cp libs/tercero.jar com.ejemplo.Main
```

##### Módulos Automáticos

Un módulo automático es un archivo JAR no modular colocado en el modulepath. Se convierte automáticamente en un módulo con un nombre basado en el nombre del archivo JAR.

###### Ejemplo de Uso de Módulos Automáticos

```bash
java --module-path libs --module com.ejemplo/com.ejemplo.Main
```

Si `tercero.jar` se encuentra en el directorio `libs`, se convierte en un módulo automático.

### Ejemplos Prácticos

#### Ejemplo Completo de Compilación y Creación de JAR Modular

1. Estructura del Proyecto:

```
src
└── com
    └── ejemplo
        ├── Main.java
        └── module-info.java
```

2. Contenido de `module-info.java`:

```java
module com.ejemplo {
    requires java.logging;
}
```

3. Contenido de `Main.java`:

```java
package com.ejemplo;

import java.util.logging.Logger;

public class Main {
    private static final Logger logger = Logger.getLogger(Main.class.getName());

    public static void main(String[] args) {
        logger.info("Hola, Mundo Modular");
    }
}
```

4. Compilación:

```bash
javac -d mods/com.ejemplo $(find src -name "*.java")
```

5. Creación del JAR:

```bash
jar --create --file=mlib/com.ejemplo.jar --module-version=1.0 -C mods/com.ejemplo .
```

6. Ejecución:

```bash
java --module-path mlib --module com.ejemplo/com.ejemplo.Main
```

#### Ejemplo de Creación de Imagen de Tiempo de Ejecución

```bash
jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.ejemplo --output miimagen
```

Ejecución de la Imagen:

```bash
miimagen/bin/java -m com.ejemplo/com.ejemplo.Main
```

### Conclusión y Consideraciones Adicionales

La gestión de módulos en Java 17 mejora la modularidad y la encapsulación del código, facilitando la creación de aplicaciones robustas y mantenibles. La capacidad de producir JARs modulares y no modulares, así como imágenes de tiempo de ejecución personalizadas, permite una distribución más eficiente y segura de aplicaciones Java.

Para dominar estos conceptos, es fundamental practicar con proyectos reales, explorando diferentes configuraciones de módulos y experimentando con la creación de JARs y imágenes de tiempo de ejecución. Además, entender cómo migrar aplicaciones existentes a un modelo modular puede ser crucial para mantener la relevancia y modernidad de las aplicaciones Java en un entorno en constante evolución.

## Desgloce de comandos

### `javac` (Compilador de Java)
- **`-d`**: Especifica el directorio donde se colocarán los archivos `.class` compilados.

#### Ejemplo:

```bash
javac -d mods/com.ejemplo $(find src -name "*.java")
```

Este comando:
- Compila todos los archivos `.java` encontrados en el directorio `src` y sus subdirectorios.
- Coloca los archivos `.class` compilados en el directorio `mods/com.ejemplo`.

### `jar` (Herramienta para Archivos JAR)

- **`cf`**: Indica al comando `jar` que cree (`c`) un nuevo archivo JAR y que incluya archivos en él (`f`).

#### Ejemplo:

```bash
jar cf ejemplo.jar -C ruta/al/directorio/clases .
```

Este comando:
- Crea (`c`) un nuevo archivo JAR llamado `ejemplo.jar`.
- Incluye (`f`) en el archivo JAR todos los archivos ubicados en el directorio especificado por `ruta/al/directorio/clases`.

- **`--create`**: Es otra forma de indicar que se quiere crear un nuevo archivo JAR. Equivalente a `c` en `cf`.
- **`--file`**: Especifica el nombre del archivo JAR que se va a crear.
- **`--module-version`**: Define la versión del módulo que se está empaquetando en el archivo JAR.

#### Ejemplo:

```bash
jar --create --file=mlib/com.ejemplo.jar --module-version=1.0 -C mods/com.ejemplo .
```

Este comando:
- Crea un nuevo archivo JAR (`--create`) llamado `mlib/com.ejemplo.jar` (`--file=mlib/com.ejemplo.jar`).
- Define la versión del módulo como `1.0` (`--module-version=1.0`).
- Incluye en el archivo JAR todos los archivos del directorio `mods/com.ejemplo`.

### `jlink` (Herramienta para Crear Imágenes de Tiempo de Ejecución)

- **`--module-path`**: Especifica el camino a los módulos.
- **`--add-modules`**: Indica los módulos que se deben incluir en la imagen de tiempo de ejecución.
- **`--output`**: Define el directorio donde se creará la imagen de tiempo de ejecución.

#### Ejemplo:

```bash
jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.ejemplo --output miimagen
```

Este comando:
- Usa `$JAVA_HOME/jmods` y `mlib` como caminos a los módulos (`--module-path $JAVA_HOME/jmods:mlib`).
- Incluye el módulo `com.ejemplo` en la imagen de tiempo de ejecución (`--add-modules com.ejemplo`).
- Crea la imagen de tiempo de ejecución en el directorio `miimagen` (`--output miimagen`).

### Desglose de Comandos en Ejemplos

#### Compilación y Creación de JAR Modular

1. **Compilación:**

```bash
javac -d mods/com.ejemplo $(find src -name "*.java")
```

- `javac`: Compilador de Java.
- `-d mods/com.ejemplo`: Coloca los archivos `.class` compilados en `mods/com.ejemplo`.
- `$(find src -name "*.java")`: Encuentra todos los archivos `.java` en el directorio `src` y sus subdirectorios.

2. **Creación del JAR:**

```bash
jar --create --file=mlib/com.ejemplo.jar --module-version=1.0 -C mods/com.ejemplo .
```

- `jar`: Herramienta para crear y manejar archivos JAR.
- `--create`: Crea un nuevo archivo JAR.
- `--file=mlib/com.ejemplo.jar`: Nombre del archivo JAR a crear.
- `--module-version=1.0`: Versión del módulo.
- `-C mods/com.ejemplo .`: Cambia al directorio `mods/com.ejemplo` y añade todos sus archivos al JAR.

3. **Ejecución del JAR Modular:**

```bash
java --module-path mlib --module com.ejemplo/com.ejemplo.Main
```

- `java`: Inicia la JVM.
- `--module-path mlib`: Especifica el camino a los módulos.
- `--module com.ejemplo/com.ejemplo.Main`: Especifica el módulo y la clase principal a ejecutar.

### Ejemplo de Creación de Imagen de Tiempo de Ejecución

```bash
jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.ejemplo --output miimagen
```

- `jlink`: Herramienta para crear imágenes de tiempo de ejecución.
- `--module-path $JAVA_HOME/jmods:mlib`: Especifica el camino a los módulos.
- `--add-modules com.ejemplo`: Añade el módulo `com.ejemplo` a la imagen.
- `--output miimagen`: Directorio donde se creará la imagen.

### Conclusión y Consideraciones Adicionales

Comprender los comandos y sus opciones es crucial para manejar eficientemente la compilación, empaquetado y despliegue de aplicaciones Java. Practicar con proyectos reales y experimentar con diferentes configuraciones te ayudará a dominar estas herramientas y a prepararte adecuadamente para la certificación de Java 17.

