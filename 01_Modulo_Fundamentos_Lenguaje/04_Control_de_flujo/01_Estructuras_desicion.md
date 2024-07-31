## Estructuras de Decisión

### 1. `if` y `else`

La estructura `if` se usa para tomar decisiones en el código basado en condiciones booleanas. Si la condición es `true`, se ejecuta el bloque de código correspondiente; de lo contrario, se omite. Se puede combinar con `else` para proporcionar un camino alternativo de ejecución.

**Sintaxis básica:**

```java
if (condición) {
    // Bloque de código si la condición es true
} else {
    // Bloque de código si la condición es false
}
```

**Ejemplo:**

```java
int x = 10;
if (x > 0) {
    System.out.println("x es positivo");
} else {
    System.out.println("x es negativo o cero");
}
```

### 2. `else if`

La cláusula `else if` se usa para evaluar múltiples condiciones en secuencia. Solo el primer bloque de `if` o `else if` cuya condición sea `true` se ejecutará.

**Sintaxis:**

```java
if (condición1) {
    // Bloque de código si la condición1 es true
} else if (condición2) {
    // Bloque de código si la condición2 es true
} else {
    // Bloque de código si ninguna condición anterior es true
}
```

**Ejemplo:**

```java
int y = 85;
if (y >= 90) {
    System.out.println("A");
} else if (y >= 80) {
    System.out.println("B");
} else if (y >= 70) {
    System.out.println("C");
} else {
    System.out.println("F");
}
```

### 3. `switch`

La estructura `switch` permite seleccionar entre múltiples opciones basadas en el valor de una variable. En Java 17, `switch` ha sido mejorado con la sintaxis de expresión `switch`, que simplifica la asignación de valores basados en casos.

**Sintaxis básica:**

```java
switch (expresión) {
    case valor1:
        // Bloque de código para caso valor1
        break;
    case valor2:
        // Bloque de código para caso valor2
        break;
    default:
        // Bloque de código si ningún caso coincide
}
```

**Ejemplo clásico:**

```java
int day = 3;
String dayName;
switch (day) {
    case 1:
        dayName = "Lunes";
        break;
    case 2:
        dayName = "Martes";
        break;
    case 3:
        dayName = "Miércoles";
        break;
    default:
        dayName = "Día inválido";
        break;
}
System.out.println(dayName); // Output: Miércoles
```

**Expresiones `switch` en Java 17:**

```java
String dayName = switch (day) {
    case 1 -> "Lunes";
    case 2 -> "Martes";
    case 3 -> "Miércoles";
    default -> "Día inválido";
};
System.out.println(dayName); // Output: Miércoles
```

### 4. Operador ternario (`? :`)

El operador ternario es una forma compacta de escribir una expresión condicional. Se compone de tres partes: una condición, un resultado si la condición es `true` y un resultado si la condición es `false`.

**Sintaxis:**

```java
variable = (condición) ? valorSiTrue : valorSiFalse;
```

**Ejemplo:**

```java
int z = 10;
String result = (z > 5) ? "Mayor que 5" : "Menor o igual a 5";
System.out.println(result); // Output: Mayor que 5
```

### Conclusión

Las estructuras de decisión en Java son fundamentales para controlar el flujo de ejecución del programa basado en condiciones específicas. `if`, `else if`, `switch` y el operador ternario permiten manejar la lógica condicional de manera clara y eficiente.

### Consideraciones Adicionales

- **Legibilidad del Código:** Usa `if-else` para condiciones simples y claras, y considera `switch` para múltiples opciones discretas.
- **Expresiones `switch`:** Las expresiones `switch` introducidas en Java 17 proporcionan una forma más concisa y clara de manejar múltiples casos.
- **Operador Ternario:** Úsalo para condiciones simples donde se necesite una asignación directa. Evita su uso en condiciones complejas para mantener la claridad del código.
- **Rendimiento:** Aunque las diferencias de rendimiento entre `if-else` y `switch` son mínimas para la mayoría de los casos, `switch` puede ser más eficiente para un gran número de opciones discretas.

