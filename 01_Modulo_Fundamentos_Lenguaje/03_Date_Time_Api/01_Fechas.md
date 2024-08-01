### Manipulación de Fechas y Horas en Java: API de Fecha y Hora

La API de Fecha y Hora en Java, introducida en Java 8 y extendida en versiones posteriores, proporciona un conjunto completo de clases para manipular fechas, horas, duraciones, períodos, instantes y zonas horarias de manera eficiente y precisa. La API se encuentra en el paquete `java.time`.

#### 1. Clases Principales

##### 1.1 `LocalDate`

La clase `LocalDate` representa una fecha sin información sobre la hora del día. Es útil para representar fechas en un formato más simple.

###### **1.1.1 Creación de `LocalDate`**

```java
LocalDate fecha = LocalDate.of(2024, 7, 30); // 30 de julio de 2024
```

###### **1.1.2 Métodos Comunes**

- `getDayOfWeek()`: Devuelve el día de la semana.

  ```java
  DayOfWeek diaDeLaSemana = fecha.getDayOfWeek(); // Resultado: TUESDAY
  ```

- `plusDays(long days)`: Añade una cantidad específica de días a la fecha.

  ```java
  LocalDate nuevaFecha = fecha.plusDays(10); // Resultado: 09 de agosto de 2024
  ```

- `minusMonths(long months)`: Resta una cantidad específica de meses a la fecha.

  ```java
  LocalDate fechaPasada = fecha.minusMonths(1); // Resultado: 30 de junio de 2024
  ```

##### 1.2 `LocalTime`

La clase `LocalTime` representa una hora del día sin información sobre la fecha.

**1.2.1 Creación de `LocalTime`**

```java
LocalTime hora = LocalTime.of(14, 30); // 14:30
```

###### **1.2.2 Métodos Comunes**

- `plusHours(long hours)`: Añade una cantidad específica de horas a la hora.

  ```java
  LocalTime nuevaHora = hora.plusHours(2); // Resultado: 16:30
  ```

- `minusMinutes(long minutes)`: Resta una cantidad específica de minutos a la hora.

  ```java
  LocalTime horaAnterior = hora.minusMinutes(15); // Resultado: 14:15
  ```

##### 1.3 `LocalDateTime`

La clase `LocalDateTime` combina `LocalDate` y `LocalTime`, representando una fecha y hora sin zona horaria.

###### **1.3.1 Creación de `LocalDateTime`**

```java
LocalDateTime fechaHora = LocalDateTime.of(2024, 7, 30, 14, 30); // 30 de julio de 2024, 14:30
```

###### **1.3.2 Métodos Comunes**

- `getDayOfMonth()`: Devuelve el día del mes.

  ```java
  int diaDelMes = fechaHora.getDayOfMonth(); // Resultado: 30
  ```

- `plusWeeks(long weeks)`: Añade una cantidad específica de semanas a la fecha y hora.

  ```java
  LocalDateTime nuevaFechaHora = fechaHora.plusWeeks(1); // Resultado: 06 de agosto de 2024, 14:30
  ```

- `minusHours(long hours)`: Resta una cantidad específica de horas a la fecha y hora.

  ```java
  LocalDateTime fechaHoraAnterior = fechaHora.minusHours(2); // Resultado: 30 de julio de 2024, 12:30
  ```

##### 1.4 `Instant`

La clase `Instant` representa un punto en el tiempo en la línea de tiempo global, en milisegundos desde el epoch (1 de enero de 1970).

###### **1.4.1 Creación de `Instant`**

```java
Instant instante = Instant.now(); // Obtiene el instante actual
```

###### **1.4.2 Métodos Comunes**

- `plus(Duration duration)`: Añade una duración específica al instante.

  ```java
  Instant futuro = instante.plus(Duration.ofHours(1)); // Resultado: Instante actual + 1 hora
  ```

- `minus(Duration duration)`: Resta una duración específica del instante.

  ```java
  Instant pasado = instante.minus(Duration.ofMinutes(30)); // Resultado: Instante actual - 30 minutos
  ```

##### 1.5 `Duration`

La clase `Duration` representa una duración en tiempo, es decir, una cantidad de tiempo entre dos instantes.

###### **1.5.1 Creación de `Duration`**

```java
Duration duracion = Duration.ofHours(2); // Duración de 2 horas
```

###### **1.5.2 Métodos Comunes**

- `toMinutes()`: Convierte la duración a minutos.

  ```java
  long minutos = duracion.toMinutes(); // Resultado: 120
  ```

- `plus(Duration duration)`: Añade una duración específica a la duración actual.

  ```java
  Duration duracionTotal = duracion.plus(Duration.ofMinutes(30)); // Resultado: Duración de 2 horas 30 minutos
  ```

##### 1.6 `Period`

La clase `Period` representa un período de tiempo en términos de años, meses y días.

###### **1.6.1 Creación de `Period`**

```java
Period periodo = Period.ofWeeks(2); // Período de 2 semanas
```

###### **1.6.2 Métodos Comunes**

- `plus(Period period)`: Añade un período específico a la fecha.

  ```java
  LocalDate fechaFutura = fecha.plus(periodo); // Resultado: Fecha actual + 2 semanas
  ```

- `minus(Period period)`: Resta un período específico de la fecha.

  ```java
  LocalDate fechaPasada = fecha.minus(Period.ofDays(10)); // Resultado: Fecha actual - 10 días
  ```

##### 1.7 `ZoneId`

La clase `ZoneId` representa una zona horaria en la región del mundo.

###### **1.7.1 Creación de `ZoneId`**

```java
ZoneId zonaHoraria = ZoneId.of("America/New_York"); // Zona horaria de Nueva York
```

###### **1.7.2 Métodos Comunes**

- `getRules()`: Devuelve las reglas de la zona horaria.

  ```java
  ZoneRules reglas = zonaHoraria.getRules();
  ```

- `getOffset(Instant instant)`: Devuelve el desfase de la zona horaria para un instante específico.

  ```java
  ZoneOffset desfase = zonaHoraria.getRules().getOffset(instante);
  ```

#### 2. Ejemplos Prácticos

**Ejemplo 1: Comparar Fechas**

```java
LocalDate fecha1 = LocalDate.of(2024, 7, 30);
LocalDate fecha2 = LocalDate.of(2024, 8, 1);
boolean esAntes = fecha1.isBefore(fecha2); // Resultado: true
```

**Ejemplo 2: Obtener la Hora Actual en una Zona Horaria Específica**

```java
ZoneId zona = ZoneId.of("Europe/Madrid");
ZonedDateTime fechaHoraZona = ZonedDateTime.now(zona);
```

**Ejemplo 3: Calcular la Duración entre Dos Instantes**

```java
Instant inicio = Instant.now();
Instant fin = inicio.plus(Duration.ofHours(5));
Duration duracion = Duration.between(inicio, fin); // Resultado: PT5H (5 horas)
```

### Conclusión y Consideraciones Adicionales

La API de Fecha y Hora en Java proporciona un conjunto robusto de herramientas para manipular fechas, horas, duraciones, períodos, instantes y zonas horarias. Las clases `LocalDate`, `LocalTime`, `LocalDateTime`, `Instant`, `Duration`, `Period`, y `ZoneId` ofrecen una solución flexible y precisa para gestionar el tiempo en aplicaciones Java. Entender y utilizar adecuadamente estas clases es esencial para el manejo efectivo de datos temporales en Java y es crucial para la certificación de Java 17.