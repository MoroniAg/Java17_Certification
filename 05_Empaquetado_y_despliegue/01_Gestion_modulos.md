### Módulos, Dependencias y Servicios en Java: Detalle Extendido

Java introdujo el sistema de módulos en la versión 9 con el Proyecto Jigsaw, que permite crear aplicaciones más seguras, escalables y mantenibles. A continuación, exploramos en detalle los conceptos clave: módulos, dependencias, exposición para reflexión, servicios, productores y consumidores.

#### Módulos en Java

Un módulo es una colección de paquetes y recursos agrupados bajo un descriptor de módulo (`module-info.java`). Cada módulo puede especificar qué paquetes exporta para ser utilizados por otros módulos y qué dependencias tiene en otros módulos.

##### Ejemplo de `module-info.java`

```java
module com.ejemplo {
    requires java.sql;
    exports com.ejemplo.paquete;
}
```

En este ejemplo, el módulo `com.ejemplo` depende del módulo `java.sql` y exporta el paquete `com.ejemplo.paquete` para que otros módulos puedan utilizarlo.

#### Dependencias de Módulos

Las dependencias entre módulos se definen mediante la palabra clave `requires`.

##### Ejemplo con Múltiples Dependencias

```java
module com.ejemplo {
    requires java.sql;
    requires java.logging;
    exports com.ejemplo.paquete;
}
```

Aquí, el módulo `com.ejemplo` requiere tanto `java.sql` como `java.logging`.

#### Exposición para Reflexión

A veces, es necesario que el contenido del módulo esté disponible para reflexión, especialmente para frameworks que dependen de la reflexión, como Hibernate o Spring. Esto se logra mediante la palabra clave `opens`.

##### Ejemplo de Apertura para Reflexión

```java
module com.ejemplo {
    requires java.sql;
    exports com.ejemplo.paquete;
    opens com.ejemplo.paquete to java.sql;
}
```

En este ejemplo, `com.ejemplo.paquete` está abierto para reflexión por `java.sql`.

#### Servicios en Java

El sistema de módulos permite la implementación y el consumo de servicios, facilitando la creación de aplicaciones modulares. Un servicio es una interfaz o clase abstracta con una o más implementaciones que pueden ser descubiertas y utilizadas por otros módulos en tiempo de ejecución.

##### Proveedor de Servicios

Un módulo puede proporcionar una implementación de un servicio utilizando la palabra clave `provides`.

```java
module com.ejemplo.productor {
    exports com.ejemplo.servicio;
    provides com.ejemplo.servicio.Servicio with com.ejemplo.impl.ServicioImpl;
}
```

En este ejemplo, `com.ejemplo.productor` proporciona `ServicioImpl` como la implementación de `Servicio`.

##### Consumidor de Servicios

Un módulo que utiliza un servicio debe declararlo con la palabra clave `uses`.

```java
module com.ejemplo.consumidor {
    requires com.ejemplo.servicio;
    uses com.ejemplo.servicio.Servicio;
}
```

El módulo `com.ejemplo.consumidor` consume `com.ejemplo.servicio.Servicio`.

#### Ejemplo Completo: Productores y Consumidores

**Productor de Servicio**

`module-info.java` del módulo productor:

```java
module com.ejemplo.productor {
    exports com.ejemplo.servicio;
    provides com.ejemplo.servicio.Servicio with com.ejemplo.impl.ServicioImpl;
}
```

Interface de Servicio:

```java
package com.ejemplo.servicio;

public interface Servicio {
    void ejecutar();
}
```

Implementación de Servicio:

```java
package com.ejemplo.impl;

import com.ejemplo.servicio.Servicio;

public class ServicioImpl implements Servicio {
    @Override
    public void ejecutar() {
        System.out.println("Servicio Ejecutado");
    }
}
```

**Consumidor de Servicio**

`module-info.java` del módulo consumidor:

```java
module com.ejemplo.consumidor {
    requires com.ejemplo.servicio;
    uses com.ejemplo.servicio.Servicio;
}
```

Clase principal que consume el servicio:

```java
package com.ejemplo.consumidor;

import com.ejemplo.servicio.Servicio;
import java.util.ServiceLoader;

public class Main {
    public static void main(String[] args) {
        ServiceLoader<Servicio> loader = ServiceLoader.load(Servicio.class);
        for (Servicio servicio : loader) {
            servicio.ejecutar();
        }
    }
}
```

### Detalles Adicionales

#### Definición y Uso de Módulos

Para definir un módulo, crea un archivo `module-info.java` en el directorio raíz del módulo. Este archivo debe contener las declaraciones `requires`, `exports`, `opens`, `provides`, y `uses` según sea necesario.

**Ejemplo Complejo de `module-info.java`**:

```java
module com.ejemplo {
    requires java.base; // Implicado por defecto
    requires java.logging;
    requires transitive java.sql;
    exports com.ejemplo.util to some.other.module;
    opens com.ejemplo.internal to framework.module;
    uses com.ejemplo.spi.ServiceProvider;
    provides com.ejemplo.spi.ServiceProvider with com.ejemplo.impl.ServiceProviderImpl;
}
```

- `requires transitive`: Indica que cualquier módulo que requiere `com.ejemplo` también requiere `java.sql`.
- `exports ... to ...`: Exporta el paquete `com.ejemplo.util` solo a `some.other.module`.
- `opens ... to ...`: Abre el paquete `com.ejemplo.internal` solo para `framework.module` para reflexión.
- `uses`: Declara que este módulo usa `com.ejemplo.spi.ServiceProvider`.
- `provides ... with ...`: Proporciona una implementación de `com.ejemplo.spi.ServiceProvider`.

#### Gestión de Servicios

El uso del sistema de módulos para servicios permite un desacoplamiento flexible. Los módulos no necesitan conocer las implementaciones específicas de los servicios que utilizan. En su lugar, pueden descubrir implementaciones en tiempo de ejecución utilizando `ServiceLoader`.

##### Ejemplo de `ServiceLoader`

```java
ServiceLoader<Servicio> loader = ServiceLoader.load(Servicio.class);
for (Servicio servicio : loader) {
    servicio.ejecutar();
}
```

Este enfoque permite que las aplicaciones encuentren y utilicen implementaciones de servicios sin necesidad de modificar el código del consumidor cuando se agregan nuevas implementaciones.

### Conclusión y Consideraciones Adicionales

El sistema de módulos en Java permite una estructura de proyecto más clara y organizada, con mejor encapsulación y gestión de dependencias. Los servicios proporcionan una manera flexible y potente de desacoplar módulos, permitiendo que las implementaciones sean descubiertas y utilizadas dinámicamente. Al comprender y utilizar estas características, se pueden crear aplicaciones Java más robustas y mantenibles.

Para prepararte para la certificación de Java 17, es fundamental que domines estos conceptos y practiques con ejemplos prácticos. Experimenta con la creación de módulos, define servicios y consumidores, y explora cómo el sistema de módulos puede mejorar la estructura y mantenibilidad de tus aplicaciones.