## Tipos de Datos Primitivos

En Java, los tipos de datos primitivos son los tipos de datos más básicos que no son objetos. Son fundamentales para el lenguaje y están optimizados para el rendimiento. Java 17 incluye ocho tipos de datos primitivos, cada uno con su tamaño y rango específicos.

### Tipos de Datos Primitivos

**1. `byte`**

- **Tamaño:** 8 bits
- **Rango:** -128 a 127
- **Descripción:** Utilizado para representar números enteros pequeños. Es útil para ahorrar memoria en grandes arreglos, donde el ahorro de espacio es crítico.

```java
byte edad = 25;
```

**2. `short`**

- **Tamaño:** 16 bits
- **Rango:** -32,768 a 32,767
- **Descripción:** Utilizado para representar números enteros más pequeños que el `int`. Puede ahorrar memoria en comparación con el `int`.

```java
short temperatura = -5;
```

**3. `int`**

- **Tamaño:** 32 bits
- **Rango:** -2,147,483,648 a 2,147,483,647
- **Descripción:** El tipo de dato entero más comúnmente utilizado. Adecuado para la mayoría de las operaciones aritméticas.

```java
int distancia = 10000;
```

**4. `long`**

- **Tamaño:** 64 bits
- **Rango:** -9,223,372,036,854,775,808 a 9,223,372,036,854,775,807
- **Descripción:** Utilizado para representar números enteros grandes. Se usa cuando el rango de `int` no es suficiente.

```java
long población = 7800000000L;
```

**5. `float`**

- **Tamaño:** 32 bits
- **Rango:** Aproximadamente ±1.4E-45 a ±3.4E38 (precisión de 7 dígitos decimales)
- **Descripción:** Tipo de dato de punto flotante de precisión simple. Se utiliza para números con decimales cuando se necesita menos precisión.

```java
float altura = 1.75f;
```

**6. `double`**

- **Tamaño:** 64 bits
- **Rango:** Aproximadamente ±4.9E-324 a ±1.8E308 (precisión de 15 dígitos decimales)
- **Descripción:** Tipo de dato de punto flotante de precisión doble. Se utiliza para números con decimales que requieren mayor precisión.

```java
double precio = 19.99;
```

**7. `char`**

- **Tamaño:** 16 bits
- **Rango:** 0 a 65,535 (representa un solo carácter Unicode)
- **Descripción:** Utilizado para representar caracteres individuales. Los caracteres se almacenan como valores Unicode.

```java
char inicial = 'J';
```

**8. `boolean`**

- **Tamaño:** No especificado (pero generalmente se almacena en 1 bit)
- **Rango:** `true` o `false`
- **Descripción:** Utilizado para representar valores lógicos. Es el tipo de dato más básico para tomar decisiones en el código.

```java
boolean esMayorDeEdad = true;
```

### Consideraciones Adicionales

- **Inicialización:** Los tipos primitivos deben ser inicializados antes de usarlos, de lo contrario, el compilador generará un error.
  
  ```java
  int numero = 10; // Inicialización correcta
  int otroNumero; // No inicializado (causará error si se usa sin asignar un valor)
  ```

- **Conversión:** Los tipos primitivos pueden ser convertidos entre sí, pero se deben tener en cuenta las posibles pérdidas de información y errores.

  ```java
  int entero = 100;
  double decimal = entero; // Conversión implícita (promoción)
  
  float flotante = (float) decimal; // Conversión explícita (casting)
  ```

- **Comparación:** Los tipos primitivos se comparan utilizando operadores relacionales como `==`, `<`, `>`, etc.

  ```java
  int a = 5;
  int b = 10;
  boolean resultado = a < b; // true
  ```
