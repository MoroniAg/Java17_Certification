### Manejar el Ciclo de Vida de los Hilos

#### Ciclo de Vida de un Hilo

Un hilo en Java pasa por varios estados durante su ciclo de vida:

1. **New (Nuevo)**: El hilo se crea pero no ha sido iniciado.
2. **Runnable (Ejecutable)**: El hilo está listo para ejecutarse y esperando ser asignado a un procesador.
3. **Blocked (Bloqueado)**: El hilo está esperando para adquirir un bloqueo.
4. **Waiting (Esperando)**: El hilo está esperando indefinidamente a que otro hilo realice una acción específica.
5. **Timed Waiting (Esperando con Tiempo)**: El hilo está esperando por un tiempo específico.
6. **Terminated (Terminado)**: El hilo ha completado su ejecución.

#### Manejo del Ciclo de Vida de los Hilos

**Creación y Ejecución de Hilos:**

```java
public class Main {
    public static void main(String[] args) {
        Thread hilo = new Thread(new MiRunnable());
        hilo.start();
    }
}

class MiRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Hilo en ejecución: " + Thread.currentThread().getName());
    }
}
```

**Estados de Bloqueo y Espera:**

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread hilo = new Thread(new MiRunnable());
        hilo.start();

        // Esperar a que el hilo termine
        hilo.join();
    }
}

class MiRunnable implements Runnable {
    @Override
    public void run() {
        synchronized (this) {
            try {
                wait(1000); // El hilo espera por 1 segundo
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### Servicios de Ejecución (Executor Services)

El framework de concurrencia de Java proporciona varios servicios de ejecución (`ExecutorService`) para gestionar el ciclo de vida de los hilos automáticamente.

**Crear un ExecutorService:**

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);
        executor.submit(new MiRunnable());
        executor.shutdown();
    }
}

class MiRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Hilo en ejecución: " + Thread.currentThread().getName());
    }
}
```

### API de Concurrencia (Concurrent API)

La API de concurrencia de Java ofrece múltiples herramientas y utilidades para gestionar hilos de manera eficiente.

#### Clases y Utilidades Comunes

**CountDownLatch:**

```java
import java.util.concurrent.CountDownLatch;

public class Main {
    public static void main(String[] args) throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(3);

        for (int i = 0; i < 3; i++) {
            new Thread(new Worker(latch)).start();
        }

        latch.await();
        System.out.println("Todos los hilos han terminado");
    }
}

class Worker implements Runnable {
    private CountDownLatch latch;

    public Worker(CountDownLatch latch) {
        this.latch = latch;
    }

    @Override
    public void run() {
        System.out.println("Hilo en ejecución: " + Thread.currentThread().getName());
        latch.countDown();
    }
}
```

**CyclicBarrier:**

```java
import java.util.concurrent.CyclicBarrier;

public class Main {
    public static void main(String[] args) {
        CyclicBarrier barrier = new CyclicBarrier(3, () -> System.out.println("Todos los hilos han llegado a la barrera"));

        for (int i = 0; i < 3; i++) {
            new Thread(new Worker(barrier)).start();
        }
    }
}

class Worker implements Runnable {
    private CyclicBarrier barrier;

    public Worker(CyclicBarrier barrier) {
        this.barrier = barrier;
    }

    @Override
    public void run() {
        System.out.println("Hilo en ejecución: " + Thread.currentThread().getName());
        try {
            barrier.await();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Exchanger:**

```java
import java.util.concurrent.Exchanger;

public class Main {
    public static void main(String[] args) {
        Exchanger<String> exchanger = new Exchanger<>();

        new Thread(new Producer(exchanger)).start();
        new Thread(new Consumer(exchanger)).start();
    }
}

class Producer implements Runnable {
    private Exchanger<String> exchanger;

    public Producer(Exchanger<String> exchanger) {
        this.exchanger = exchanger;
    }

    @Override
    public void run() {
        try {
            String message = "Hola desde el productor";
            exchanger.exchange(message);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

class Consumer implements Runnable {
    private Exchanger<String> exchanger;

    public Consumer(Exchanger<String> exchanger) {
        this.exchanger = exchanger;
    }

    @Override
    public void run() {
        try {
            String message = exchanger.exchange(null);
            System.out.println("Consumidor recibió: " + message);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

### Conclusión y Consideraciones Adicionales

Manejar el ciclo de vida de los hilos y utilizar la API de concurrencia en Java es crucial para desarrollar aplicaciones robustas y eficientes. Los servicios de ejecución (`ExecutorService`) proporcionan una manera sencilla de gestionar hilos y tareas concurrentes, mientras que las utilidades de la API de concurrencia como `CountDownLatch`, `CyclicBarrier`, y `Exchanger` facilitan la coordinación entre hilos. Practicar con estos conceptos y herramientas te permitirá dominar la concurrencia en Java y estar mejor preparado para la certificación de Java 17.