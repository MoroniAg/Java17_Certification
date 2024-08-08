### Crear Hilos de Trabajo con Runnable y Callable

#### 1. Crear Hilos usando Runnable

La interfaz `Runnable` es una interfaz funcional en Java que se utiliza para definir una tarea que puede ser ejecutada por un hilo. Contiene un solo método, `run()`, que no toma argumentos y no devuelve ningún valor.

**Definición de una Clase Runnable:**

```java
public class MiRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Hilo en ejecución: " + Thread.currentThread().getName());
    }
}
```

**Ejecutar una Tarea Runnable:**

Para ejecutar esta tarea en un hilo, puedes utilizar la clase `Thread`:

```java
public class Main {
    public static void main(String[] args) {
        Thread hilo = new Thread(new MiRunnable());
        hilo.start();
    }
}
```

#### 2. Crear Hilos usando Callable

`Callable` es otra interfaz funcional en Java que es similar a `Runnable`, pero a diferencia de `Runnable`, `Callable` puede devolver un valor y puede lanzar una excepción.

**Definición de una Clase Callable:**

```java
import java.util.concurrent.Callable;

public class MiCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        return "Resultado del hilo: " + Thread.currentThread().getName();
    }
}
```

**Ejecutar una Tarea Callable:**

Para ejecutar una tarea `Callable`, generalmente se utiliza un `ExecutorService`:

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class Main {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<String> futuro = executor.submit(new MiCallable());
        System.out.println(futuro.get());
        executor.shutdown();
    }
}
```

#### Ejemplo Completo con Varios Hilos

A continuación, se muestra un ejemplo completo que crea y ejecuta varias tareas `Runnable` y `Callable` utilizando un `ExecutorService`.

**Ejemplo Completo:**

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class Main {
    public static void main(String[] args) throws Exception {
        // Crear un ExecutorService con un pool de hilos fijo
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Crear y ejecutar tareas Runnable
        for (int i = 0; i < 5; i++) {
            executor.submit(new MiRunnable());
        }

        // Crear y ejecutar tareas Callable
        Future<String> future1 = executor.submit(new MiCallable());
        Future<String> future2 = executor.submit(new MiCallable());

        // Obtener y mostrar los resultados de las tareas Callable
        System.out.println(future1.get());
        System.out.println(future2.get());

        // Cerrar el ExecutorService
        executor.shutdown();
    }
}

class MiRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Hilo en ejecución: " + Thread.currentThread().getName());
    }
}

class MiCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        return "Resultado del hilo: " + Thread.currentThread().getName();
    }
}
```

### Conclusión y Consideraciones Adicionales

Entender cómo crear y manejar hilos usando `Runnable` y `Callable` es esencial para el desarrollo concurrente en Java. `Runnable` es más simple y no devuelve resultados, mientras que `Callable` puede devolver un resultado y lanzar excepciones. Utilizar un `ExecutorService` facilita la gestión de hilos y la ejecución de tareas en paralelo, mejorando el rendimiento y la capacidad de respuesta de las aplicaciones. Es fundamental practicar estos conceptos y adaptarlos a tus necesidades específicas para dominar su uso y estar preparado para la certificación de Java 17.