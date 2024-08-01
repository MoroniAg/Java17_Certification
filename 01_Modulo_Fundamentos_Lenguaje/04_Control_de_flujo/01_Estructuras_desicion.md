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
#### 3.1 Estructura `swith`
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

#### 3.2 Expresiones `switch` 

Las expresiones `switch` permiten evaluar una expresión y devolver un valor basado en el resultado de esa evaluación. Esta característica proporciona una sintaxis más limpia y evita la necesidad de múltiples sentencias `break`.

##### Sintaxis Básica de Expresiones `switch`

```java
var resultado = switch (expresion) {
    case valor1 -> "Resultado 1";
    case valor2 -> "Resultado 2";
    // Otros casos
    default -> "Resultado por defecto";
};
```

En este contexto, `expresion` es evaluada y el valor correspondiente se asigna a `resultado`.

##### Ejemplo de Expresión `switch`

```java
int mes = 4;
String nombreMes = switch (mes) {
    case 1 -> "Enero";
    case 2 -> "Febrero";
    case 3 -> "Marzo";
    case 4 -> "Abril";
    case 5 -> "Mayo";
    case 6 -> "Junio";
    case 7 -> "Julio";
    case 8 -> "Agosto";
    case 9 -> "Septiembre";
    case 10 -> "Octubre";
    case 11 -> "Noviembre";
    case 12 -> "Diciembre";
    default -> "Mes inválido";
};
System.out.println("El mes es: " + nombreMes);
```

En este ejemplo, se imprimirá "El mes es: Abril" porque la variable `mes` tiene el valor `4`.

##### Uso de Bloques de Código con Expresiones `switch`

En las expresiones `switch`, también puedes usar bloques de código y `yield` para devolver valores. Esto es útil cuando necesitas realizar operaciones adicionales antes de devolver un resultado.

**Ejemplo:**

```java
int mes = 2;
int year = 2024;
int diasEnMes = switch (mes) {
    case 1, 3, 5, 7, 8, 10, 12 -> 31;
    case 4, 6, 9, 11 -> 30;
    case 2 -> {
        if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
            yield 29; // Año bisiesto
        } else {
            yield 28;
        }
    }
    default -> 0;
};
System.out.println("Días en el mes: " + diasEnMes);
```

En este ejemplo, se imprimirá "Días en el mes: 29" porque el año 2024 es bisiesto.

##### Conclusión y Consideraciones Adicionales

Las expresiones `switch` en Java proporcionan una forma más moderna y eficiente de manejar múltiples condiciones en comparación con la estructura `switch` clásica. Permiten una sintaxis más concisa y clara, lo que mejora la legibilidad del código y reduce la posibilidad de errores comunes como la omisión de sentencias `break`. Para aquellos que se preparan para la certificación de Java 17, es esencial comprender y dominar tanto las estructuras de control tradicionales como estas nuevas expresiones para escribir código robusto y eficiente.

### 4. `yield`

El `yield` en las expresiones `switch` es una nueva palabra clave introducida en Java 14 que permite devolver un valor desde un bloque de código dentro de una expresión `switch`. A diferencia del `return`, que se utiliza para salir de un método y devolver un valor, `yield` se utiliza dentro de una expresión `switch` para especificar el valor que debe ser devuelto por el `switch` cuando se selecciona un caso específico.

#### Uso de `yield` en Expresiones `switch`

Cuando utilizas un bloque de código en una expresión `switch`, puedes usar `yield` para devolver un valor desde ese bloque. Esto es especialmente útil cuando necesitas realizar cálculos o evaluaciones adicionales antes de determinar el valor a devolver.

#### Ejemplo Básico

```java
int mes = 2;
int year = 2024;
int diasEnMes = switch (mes) {
    case 1, 3, 5, 7, 8, 10, 12 -> 31;
    case 4, 6, 9, 11 -> 30;
    case 2 -> {
        if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
            yield 29; // Año bisiesto
        } else {
            yield 28;
        }
    }
    default -> 0;
};
System.out.println("Días en el mes: " + diasEnMes);
```

En este ejemplo, para el caso `2`, el bloque de código verifica si el año es bisiesto y utiliza `yield` para devolver 29 si lo es, o 28 si no lo es.

#### Ventajas de `yield`

1. **Claridad y Concisión**: Permite escribir expresiones `switch` más claras y concisas.
2. **Flexibilidad**: Facilita la ejecución de lógica compleja dentro de una expresión `switch` antes de devolver un valor.
3. **Manejo de Bloques**: Permite manejar casos que requieren múltiples líneas de código antes de determinar el valor a devolver.

#### Comparación con `return`

Mientras que `return` se usa para salir de un método y devolver un valor a la llamada del método, `yield` se usa dentro de una expresión `switch` para devolver un valor desde un caso específico sin salir del método.

**Ejemplo de Uso de `return` vs `yield`**:

**Con `return`:**

```java
public int obtenerDiasEnMes(int mes, int year) {
    switch (mes) {
        case 1: case 3: case 5: case 7: case 8: case 10: case 12:
            return 31;
        case 4: case 6: case 9: case 11:
            return 30;
        case 2:
            if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
                return 29;
            } else {
                return 28;
            }
        default:
            return 0;
    }
}
```

**Con `yield`:**

```java
int mes = 2;
int year = 2024;
int diasEnMes = switch (mes) {
    case 1, 3, 5, 7, 8, 10, 12 -> 31;
    case 4, 6, 9, 11 -> 30;
    case 2 -> {
        if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
            yield 29;
        } else {
            yield 28;
        }
    }
    default -> 0;
};
System.out.println("Días en el mes: " + diasEnMes);
```

#### Conclusión y Consideraciones Adicionales

El uso de `yield` en expresiones `switch` proporciona una forma poderosa y flexible de devolver valores desde un `switch` en Java. Esta funcionalidad mejora la legibilidad y la claridad del código, permitiendo manejar casos complejos de manera más eficiente. Es esencial para aquellos que se preparan para la certificación de Java 17 comprender y ser capaces de aplicar `yield` en expresiones `switch` para escribir código moderno y eficiente.

### 5. Operador ternario (`? :`)

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

