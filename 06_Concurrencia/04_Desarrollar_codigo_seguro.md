### Desarrollar Código Seguro para Hilos

Desarrollar código seguro para hilos (thread-safe) es crucial para evitar problemas de concurrencia, como condiciones de carrera y problemas de visibilidad. En Java, hay varias técnicas y mecanismos de bloqueo para asegurar la seguridad de los hilos.

#### Sincronización

**Métodos Synchronized:**

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

**Bloques Synchronized:**

```java
public class Counter {
    private int count = 0;
    private final Object lock = new Object();

    public void increment() {
        synchronized (lock) {
            count++;
        }
    }

    public int getCount() {
        synchronized (lock) {
            return count;
        }
    }
}
```

#### Clases de Bloqueo (Lock Classes)

**ReentrantLock:**

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
        lock.lock();
        try {
            return count;
        } finally {
            lock.unlock();
        }
    }
}
```

**ReentrantReadWriteLock:**

```java
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class Counter {
    private int count = 0;
    private final ReadWriteLock lock = new ReentrantReadWriteLock();

    public void increment() {
        lock.writeLock().lock();
        try {
            count++;
        } finally {
            lock.writeLock().unlock();
        }
    }

    public int getCount() {
        lock.readLock().lock();
        try {
            return count;
        } finally {
            lock.readLock().unlock();
        }
    }
}
```

### API Concurrente de Java

La API de concurrencia de Java proporciona diversas clases y utilidades para manejar la sincronización y el bloqueo.

#### Colecciones Concurrentes

**ConcurrentHashMap:**

```java
import java.util.concurrent.ConcurrentHashMap;

public class Main {
    public static void main(String[] args) {
        ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();

        map.put("a", 1);
        map.put("b", 2);

        System.out.println(map.get("a"));
    }
}
```

#### Atomic Variables

Las variables atómicas permiten operaciones atómicas en variables de tipo primitivo y referencias de objetos.

**AtomicInteger:**

```java
import java.util.concurrent.atomic.AtomicInteger;

public class Counter {
    private AtomicInteger count = new AtomicInteger(0);

    public void increment() {
        count.incrementAndGet();
    }

    public int getCount() {
        return count.get();
    }
}
```

**AtomicReference:**

```java
import java.util.concurrent.atomic.AtomicReference;

public class Counter {
    private AtomicReference<Integer> count = new AtomicReference<>(0);

    public void increment() {
        count.updateAndGet(value -> value + 1);
    }

    public int getCount() {
        return count.get();
    }
}
```

#### Ejemplo Completo

```java
import java.util.concurrent.Executors;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.locks.ReentrantLock;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        executor.submit(task);
        executor.submit(task);

        executor.shutdown();

        while (!executor.isTerminated()) {}

        System.out.println("Final count: " + counter.getCount());
    }
}

class Counter {
    private int count = 0;
    private final ReentrantLock lock = new ReentrantLock();

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

### Conclusión y Consideraciones Adicionales

Desarrollar código seguro para hilos implica una comprensión profunda de los mecanismos de bloqueo y la API concurrente de Java. Utilizar `synchronized`, `Lock`, y colecciones concurrentes adecuadamente garantiza que las aplicaciones sean seguras y eficientes en entornos multihilo. Practicar con estos conceptos y ejemplos es fundamental para dominar la concurrencia en Java y estar mejor preparado para la certificación de Java 17.