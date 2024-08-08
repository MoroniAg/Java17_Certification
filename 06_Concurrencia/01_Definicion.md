### Managing Concurrent Code Execution en Java

La gestión de la ejecución concurrente del código es esencial en aplicaciones que requieren realizar múltiples tareas simultáneamente. Java proporciona varias herramientas y bibliotecas para manejar la concurrencia de manera eficiente y segura.

#### Conceptos Clave

1. **Concurrencia**: Capacidad de un programa para ejecutar múltiples tareas de manera simultánea, mejorando la eficiencia y el rendimiento.
2. **Paralelismo**: Subconjunto de la concurrencia donde múltiples tareas se ejecutan verdaderamente al mismo tiempo, típicamente en un sistema multi-core.

### Herramientas y Técnicas en Java

#### 1. **Threads (Hilos)**

- **Definición**: Un hilo es la unidad más pequeña de procesamiento programable. En Java, se puede crear un hilo extendiendo la clase `Thread` o implementando la interfaz `Runnable`.
- **Uso Básico**:
  ```java
  class MyThread extends Thread {
      public void run() {
          System.out.println("Hilo en ejecución");
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.start();
      }
  }
  ```

#### 2. **Runnable e Callable**

- **Runnable**: Interfaz funcional que define un único método `run()`, que no retorna valor ni puede lanzar excepciones.
  ```java
  class MyRunnable implements Runnable {
      public void run() {
          System.out.println("Runnable en ejecución");
      }
  }
  ```
- **Callable**: Similar a `Runnable`, pero puede retornar un valor y lanzar excepciones.
  ```java
  import java.util.concurrent.Callable;

  class MyCallable implements Callable<Integer> {
      public Integer call() throws Exception {
          return 123;
      }
  }
  ```

#### 3. **Executor Framework**

- **Definición**: Proporciona una forma más flexible y poderosa de gestionar hilos. El framework incluye varias implementaciones de interfaces como `Executor`, `ExecutorService`, y `ScheduledExecutorService`.
- **Uso Básico**:
  ```java
  import java.util.concurrent.ExecutorService;
  import java.util.concurrent.Executors;

  public class Main {
      public static void main(String[] args) {
          ExecutorService executor = Executors.newFixedThreadPool(10);
          executor.submit(() -> {
              System.out.println("Tarea en ejecución");
          });
          executor.shutdown();
      }
  }
  ```

#### 4. **Futures y CompletionStage**

- **Future**: Representa el resultado de una operación asincrónica. Permite comprobar si la operación ha completado, esperar su finalización, y obtener su resultado.
  ```java
  import java.util.concurrent.*;

  public class Main {
      public static void main(String[] args) throws Exception {
          ExecutorService executor = Executors.newSingleThreadExecutor();
          Future<Integer> future = executor.submit(() -> 123);
          Integer result = future.get(); // Espera hasta que la tarea complete y obtiene el resultado
          System.out.println(result);
          executor.shutdown();
      }
  }
  ```

- **CompletionStage**: Parte del API de `CompletableFuture`, que permite la programación funcional de tareas asincrónicas.
  ```java
  import java.util.concurrent.CompletableFuture;

  public class Main {
      public static void main(String[] args) {
          CompletableFuture.supplyAsync(() -> "Hola")
                           .thenApplyAsync(s -> s + " Mundo")
                           .thenAcceptAsync(System.out::println);
      }
  }
  ```

#### 5. **Synchronized y Locks**

- **Synchronized**: Palabra clave utilizada para asegurar que sólo un hilo puede ejecutar un bloque de código o método sincronizado en un momento dado.
  ```java
  public class Counter {
      private int count = 0;

      public synchronized void increment() {
          count++;
      }

      public synchronized int getCount() {
          return count;
      }
  }
  ```

- **Locks**: Proporcionan una forma más flexible y sofisticada de control de acceso que los bloques sincronizados.
  ```java
  import java.util.concurrent.locks.Lock;
  import java.util.concurrent.locks.ReentrantLock;

  public class Counter {
      private int count = 0;
      private final Lock lock = new ReentrantLock();

      public void increment() {
          lock.lock();
          try {
              count++;
          } finally {
              lock.unlock();
          }
      }

      public int getCount() {
          return count;
      }
  }
  ```

### Consideraciones de Concurrencia

1. **Race Conditions**: Ocurren cuando múltiples hilos acceden y manipulan un recurso compartido sin la adecuada sincronización, llevando a resultados inconsistentes.
2. **Deadlocks**: Situación en la cual dos o más hilos están bloqueados para siempre, esperando unos por otros para liberar los recursos.
3. **Livelocks**: Situación donde dos o más hilos siguen cambiando de estado en respuesta a los cambios de estado de otros hilos, sin hacer ningún progreso.
4. **Starvation**: Cuando un hilo no puede acceder a los recursos necesarios para progresar debido a que otros hilos acaparan esos recursos.

### Conclusión

El manejo de la ejecución concurrente en Java es crucial para aplicaciones que requieren eficiencia y rendimiento mejorado. Utilizar adecuadamente los hilos, el framework `Executor`, `Future`, `CompletableFuture`, y mecanismos de sincronización permite desarrollar aplicaciones concurrentes robustas y eficientes. Es esencial tener en cuenta los problemas potenciales como condiciones de carrera, deadlocks y starvation, y emplear las mejores prácticas para evitarlos.

