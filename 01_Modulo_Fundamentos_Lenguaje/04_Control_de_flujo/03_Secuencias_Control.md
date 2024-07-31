## Sentencias de Control

Las sentencias de control permiten modificar el flujo de ejecución dentro de los bucles y métodos. En Java, las principales sentencias de control son `break`, `continue` y `return`.

### 1. `break`

La sentencia `break` se utiliza para salir de un bucle antes de que la condición del bucle se vuelva falsa. También se puede usar en una estructura `switch` para terminar un caso.

**Sintaxis básica:**

*break;*

**Ejemplo en un bucle `for`:**
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break; // Sale del bucle cuando i es 5
    }
    System.out.println(i);
}
```
**Ejemplo en una estructura `switch`:**
```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Lunes");
        break;
    case 2:
        System.out.println("Martes");
        break;
    case 3:
        System.out.println("Miércoles");
        break;
    default:
        System.out.println("Día inválido");
        break;
}
```
### 2. `continue`

La sentencia `continue` se utiliza para saltar la iteración actual de un bucle y pasar a la siguiente iteración. Se usa principalmente dentro de bucles `for`, `while` y `do-while`.

**Sintaxis básica:**

*continue;*

**Ejemplo en un bucle `for`:**
```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue; // Salta la iteración actual si i es par
    }
    System.out.println(i); // Imprime solo números impares
}
```
### 3. `return`

La sentencia `return` se utiliza para salir de un método y opcionalmente devolver un valor al método que lo llamó. Es crucial para controlar el flujo de los métodos y funciones.

**Sintaxis básica:**
```java
return; (para métodos `void`)

return valor; (para métodos que devuelven un valor)
```
**Ejemplo en un método `void`:**

```java
public void checkNumber(int num) {
    if (num < 0) {
        System.out.println("Número negativo");
        return; // Sale del método si el número es negativo
    }
    System.out.println("Número positivo");
}
```

**Ejemplo en un método que devuelve un valor:**

```java
public int add(int a, int b) {
    return a + b; // Devuelve la suma de a y b
}
```

### Ejemplos Completos

Aquí tienes ejemplos completos que demuestran el uso de `break`, `continue` y `return` en diferentes contextos:

**Uso de `break` en un bucle `for`:**

```java
public class EjemploBreak {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i == 5) {
                break;
            }
            System.out.println(i);
        }
    }
}
```

**Uso de `continue` en un bucle `for`:**

```java
public class EjemploContinue {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i % 2 == 0) {
                continue;
            }
            System.out.println(i);
        }
    }
}
```

**Uso de `return` en métodos:**

```java
public class EjemploReturn {
    public static void main(String[] args) {
        checkNumber(-5);
        int result = add(3, 7);
        System.out.println("Resultado de la suma: " + result);
    }

    public static void checkNumber(int num) {
        if (num < 0) {
            System.out.println("Número negativo");
            return;
        }
        System.out.println("Número positivo");
    }

    public static int add(int a, int b) {
        return a + b;
    }
}
```

### Conclusión

Las sentencias de control `break`, `continue` y `return` son fundamentales para gestionar el flujo de ejecución en bucles y métodos. Cada una tiene un propósito específico que, cuando se usa correctamente, mejora la claridad y eficiencia del código.

### Consideraciones Adicionales

- **Uso Apropiado de `break`:** Utiliza `break` para salir de bucles cuando se cumplan ciertas condiciones específicas, evitando iteraciones innecesarias.
- **Evitar `continue` Excesivo:** Aunque `continue` es útil para omitir iteraciones específicas, un uso excesivo puede hacer que el flujo del bucle sea difícil de seguir.
- **Retorno en Métodos:** Asegúrate de que los métodos que devuelven valores siempre usen `return` para proporcionar los resultados esperados. Para métodos `void`, `return` se utiliza para salir del método antes de tiempo si es necesario.
