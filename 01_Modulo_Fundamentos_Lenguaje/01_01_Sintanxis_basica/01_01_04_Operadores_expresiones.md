## Operadores y Expresiones

### Operadores

Los operadores en Java permiten realizar operaciones sobre variables y valores. Aquí se detallan los principales operadores disponibles:

#### **1. Operadores Aritméticos**

Realizan operaciones matemáticas básicas.

- **Suma (`+`):** Suma dos operandos.

  ```java
  int suma = 5 + 3; // Resultado: 8
  ```

- **Resta (`-`):** Resta el segundo operando del primero.

  ```java
  int resta = 10 - 4; // Resultado: 6
  ```

- **Multiplicación (`*`):** Multiplica dos operandos.

  ```java
  int multiplicacion = 7 * 2; // Resultado: 14
  ```

- **División (`/`):** Divide el primer operando por el segundo. (En enteros, la división descarta el residuo.)

  ```java
  int division = 9 / 3; // Resultado: 3
  ```

- **Módulo (`%`):** Calcula el residuo de la división del primer operando por el segundo.

  ```java
  int modulo = 10 % 3; // Resultado: 1
  ```

#### **2. Operadores Relacionales**

Comparan dos operandos y devuelven un valor booleano (`true` o `false`).

- **Igual a (`==`):** Comprueba si dos operandos son iguales.

  ```java
  boolean igual = (5 == 5); // Resultado: true
  ```

- **Distinto de (`!=`):** Comprueba si dos operandos son diferentes.

  ```java
  boolean distinto = (5 != 3); // Resultado: true
  ```

- **Mayor que (`>`):** Comprueba si el primer operando es mayor que el segundo.

  ```java
  boolean mayor = (7 > 4); // Resultado: true
  ```

- **Menor que (`<`):** Comprueba si el primer operando es menor que el segundo.

  ```java
  boolean menor = (3 < 8); // Resultado: true
  ```

- **Mayor o igual que (`>=`):** Comprueba si el primer operando es mayor o igual que el segundo.

  ```java
  boolean mayorIgual = (5 >= 5); // Resultado: true
  ```

- **Menor o igual que (`<=`):** Comprueba si el primer operando es menor o igual que el segundo.

  ```java
  boolean menorIgual = (6 <= 8); // Resultado: true
  ```

#### **3. Operadores Lógicos**

Operan sobre valores booleanos.

- **AND lógico (`&&`):** Devuelve `true` si ambos operandos son `true`.

  ```java
  boolean and = (true && false); // Resultado: false
  ```

- **OR lógico (`||`):** Devuelve `true` si al menos uno de los operandos es `true`.

  ```java
  boolean or = (true || false); // Resultado: true
  ```

- **NOT lógico (`!`):** Invierte el valor booleano del operando.

  ```java
  boolean not = !true; // Resultado: false
  ```

#### **4. Operadores de Asignación**

Se utilizan para asignar valores a variables.

- **Asignación simple (`=`):** Asigna el valor del operando derecho a la variable del operando izquierdo.

  ```java
  int a = 10;
  ```

- **Asignación con suma (`+=`):** Suma el valor del operando derecho a la variable del operando izquierdo y asigna el resultado.

  ```java
  int b = 5;
  b += 3; // Equivalente a b = b + 3; Resultado: b = 8
  ```

- **Asignación con multiplicación (`*=`):** Multiplica el valor del operando derecho con la variable del operando izquierdo y asigna el resultado.

  ```java
  int c = 4;
  c *= 2; // Equivalente a c = c * 2; Resultado: c = 8
  ```

#### **5. Operadores Unarios**

Los operadores unarios en Java son operadores que operan sobre un solo operando. Estos operadores realizan varias funciones como la negación, el incremento, el decremento, entre otras. A continuación, se detallan los operadores unarios disponibles en Java y se proporcionan ejemplos para ilustrar su funcionamiento.

##### 5.1. Incremento (`++`)

El operador de incremento aumenta el valor de su operando en 1. Puede usarse en dos formas: prefijo y sufijo.

- **Prefijo (`++variable`)**: Incrementa la variable antes de utilizar su valor en la expresión.
  
  ```java
  int a = 5;
  int b = ++a; // a se incrementa a 6, luego b se asigna el valor de a, que es 6
  ```

- **Sufijo (`variable++`)**: Utiliza el valor de la variable en la expresión antes de incrementarla.

  ```java
  int c = 5;
  int d = c++; // d se asigna el valor de c, que es 5, luego c se incrementa a 6
  ```

##### 5.2. Decremento (`--`)

El operador de decremento disminuye el valor de su operando en 1. También puede usarse en dos formas: prefijo y sufijo.

- **Prefijo (`--variable`)**: Decrementa la variable antes de utilizar su valor en la expresión.
  
  ```java
  int e = 5;
  int f = --e; // e se decrementa a 4, luego f se asigna el valor de e, que es 4
  ```

- **Sufijo (`variable--`)**: Utiliza el valor de la variable en la expresión antes de decrementarla.

  ```java
  int g = 5;
  int h = g--; // h se asigna el valor de g, que es 5, luego g se decrementa a 4
  ```

##### 5.3. Negación (`-`)

El operador de negación cambia el signo del operando.

```java
int i = 10;
int j = -i; // j es -10
```

##### 5.4. Complemento (`~`)

El operador de complemento invierte todos los bits del operando. Este es un operador bit a bit.

```java
int k = 5;       // 5 es 00000000 00000000 00000000 00000101 en binario
int l = ~k;      // l es 11111111 11111111 11111111 11111010 en binario (complemento de 2)
```

##### 5.5. Negación Lógica (`!`)

El operador de negación lógica invierte el valor booleano del operando.

```java
boolean m = true;
boolean n = !m; // n es false
```

##### 5.6. Ejemplo Completo

Aquí tienes un ejemplo completo que demuestra el uso de los operadores unarios en Java:

```java
public class OperadoresUnarios {

    public static void main(String[] args) {
        int a = 5;

        // Incremento
        System.out.println("a: " + a);       // 5
        System.out.println("++a: " + ++a);   // 6
        System.out.println("a++: " + a++);   // 6
        System.out.println("a: " + a);       // 7

        // Decremento
        System.out.println("--a: " + --a);   // 6
        System.out.println("a--: " + a--);   // 6
        System.out.println("a: " + a);       // 5

        // Negación
        int b = -a;
        System.out.println("-a: " + b);      // -5

        // Complemento
        int c = 5;
        System.out.println("~c: " + ~c);     // -6 (complemento de 2)

        // Negación lógica
        boolean d = true;
        System.out.println("!d: " + !d);     // false
    }
}
```

##### 5.7. Conclusión

Los operadores unarios son herramientas poderosas y convenientes para manipular valores directamente. Su correcto entendimiento y uso pueden simplificar muchas operaciones comunes en programación, mejorando la eficiencia y la legibilidad del código.

##### 5.8. Consideraciones Adicionales

- **Prefijo vs Sufijo**: Comprende la diferencia entre el uso de operadores prefijos y sufijos, ya que pueden tener impactos significativos en expresiones complejas.
- **Uso del Complemento**: El operador de complemento es menos común en el desarrollo de aplicaciones estándar, pero es esencial en programación de bajo nivel y en ciertas aplicaciones de algoritmos.
- **Claridad del Código**: Usa operadores unarios de manera que mantengan la claridad del código, evitando el uso excesivo en expresiones complicadas que puedan confundir a otros desarrolladores.


#### **6. Operadores de Tipo**

Permiten convertir tipos de datos.


##### **6.1. Casting:** 
El *casting* es el proceso de convertir una variable de un tipo de datos a otro. Java soporta dos tipos principales de *casting*: el *casting* implícito y el *casting* explícito.

- **Casting Implícito:** También conocido como *widening* o *upcasting*, es el tipo de *casting* que se realiza automáticamente cuando se pasa de un tipo de dato más pequeño a uno más grande. Por ejemplo, de `int` a `long`.

  ```java
  int a = 100;
  long b = a; // Casting implícito de int a long
  ```

- **Casting Explícito:** También conocido como *narrowing* o *downcasting*, es el tipo de *casting* que debe ser especificado explícitamente en el código, ya que puede resultar en pérdida de datos o errores. Por ejemplo, de `double` a `int`.

###### 6.1.1 Casting Explícito

El *casting* explícito es necesario cuando se desea convertir un tipo de datos más grande a uno más pequeño, o cuando se quiere asegurar que la conversión se realiza de manera controlada.

**Sintaxis:**

```java
targetType variableName = (targetType) valueToBeCast;
```

###### 6.1.2. Ejemplos de Casting Explícito

1. **De `double` a `int`**

```java
double pi = 3.14159;
int intPi = (int) pi; // El valor de intPi será 3, perdiendo la parte decimal
```

2. **De `long` a `short`**

```java
long largeValue = 123456789L;
short smallValue = (short) largeValue; // El valor de smallValue será -13035 debido a la pérdida de datos
```

3. **De `float` a `byte`**

```java
float f = 128.56f;
byte b = (byte) f; // El valor de b será -128, debido a la pérdida de datos
```

4. **Casting entre clases (con herencia)**

Cuando se trabaja con clases y herencia, el *casting* puede ser necesario para convertir entre tipos de objetos. 

```java
class Animal {
    void makeSound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Woof");
    }
}

public class TestCasting {
    public static void main(String[] args) {
        Animal myAnimal = new Dog();
        Dog myDog = (Dog) myAnimal; // Casting explícito de Animal a Dog
        myDog.bark(); // Llamada al método específico de Dog
    }
}
```

###### 6.1.3. Consideraciones y Riesgos del Casting Explícito

1. **Pérdida de Datos:** Al convertir tipos más grandes a tipos más pequeños, puede ocurrir una pérdida significativa de datos. Por ejemplo, al convertir un `double` a un `int`, se pierde la parte decimal.

2. **Errores de Ejecución:** Si el *casting* no es válido, puede provocar errores en tiempo de ejecución. Por ejemplo, intentar convertir un objeto de una clase a una clase no relacionada causará un `ClassCastException`.

3. **Verificación de Tipo:** Es recomendable verificar el tipo antes de realizar un *casting* utilizando el operador `instanceof` para evitar excepciones en tiempo de ejecución. 

   ```java
   if (myAnimal instanceof Dog) {
       Dog myDog = (Dog) myAnimal;
       myDog.bark();
   } else {
       System.out.println("El objeto no es una instancia de Dog");
   }
   ``` 
   **Instanceof:** Comprueba si un objeto es una instancia de una clase o interfaz específica.
   ```java
   String texto = "Hola";
   boolean esString = texto instanceof String; // Resultado: true
   ```
###### 6.1.4. Ejemplo Completo

Aquí tienes un ejemplo que muestra diferentes tipos de *casting* explícito:

```java
public class CastingEjemplo {

    public static void main(String[] args) {
        // Casting de double a int
        double valorDouble = 9.78;
        int valorInt = (int) valorDouble; // ValorInt será 9
        System.out.println("Double a int: " + valorInt);

        // Casting de long a short
        long valorLong = 100000;
        short valorShort = (short) valorLong; // ValorShort será 34464
        System.out.println("Long a short: " + valorShort);

        // Casting entre clases con herencia
        Animal miAnimal = new Dog();
        if (miAnimal instanceof Dog) {
            Dog miPerro = (Dog) miAnimal;
            miPerro.bark(); // Output: Woof
        }
    }
}
```

###### 6.1.5. Conclusión

El *casting* explícito es una herramienta poderosa en Java que permite la conversión de tipos de datos. Es fundamental comprender cuándo y cómo usar el *casting* explícito para evitar pérdida de datos y errores en tiempo de ejecución.

###### 6.1.6. Consideraciones Adicionales

- **Uso de `instanceof`:** Utiliza `instanceof` para verificar el tipo antes de hacer un *casting* para prevenir excepciones.
- **Pérdida de Precisión:** Ten en cuenta que el *casting* de tipos de punto flotante a enteros resulta en pérdida de la parte decimal.
- **Manejo de Excepciones:** Maneja posibles `ClassCastException` adecuadamente para mantener la robustez del programa.

### Expresiones

Una expresión en Java es una combinación de variables, literales y operadores que se evalúan para obtener un valor. Las expresiones pueden ser simples o complejas y se utilizan en diversas partes del código, como en asignaciones, condiciones y bucles.

#### **1. Expresiones Aritméticas**

Combina operadores aritméticos y operandos.

```java
int resultado = (5 + 3) * 2; // Resultado: 16
```

#### **2. Expresiones Relacionales**

Utilizan operadores relacionales para comparar valores.

```java
boolean esMayor = (10 > 5); // Resultado: true
```

#### **3. Expresiones Lógicas**

Utilizan operadores lógicos para combinar condiciones booleanas.

```java
boolean resultadoLogico = (true && (5 > 3)); // Resultado: true
```

#### **4. Expresiones Condicionales**

Utilizan el operador ternario (`? :`) para realizar una selección condicional.

```java
int max = (a > b) ? a : b; // Devuelve el valor mayor entre a y b
```

### Ejemplo Completo

```java
public class OperadoresEjemplo {

    public static void main(String[] args) {
        int a = 10;
        int b = 5;

        // Operadores Aritméticos
        int suma = a + b; // 15
        int producto = a * b; // 50

        // Operadores Relacionales
        boolean esIgual = (a == b); // false

        // Operadores Lógicos
        boolean resultadoLogico = (a > 0 && b < 10); // true

        // Operadores Unarios
        int incremento = a++;
        int decremento = --b;

        // Operadores de Asignación
        a += 5; // a = 15
        b *= 2; // b = 10

        // Expresiones
        int max = (a > b) ? a : b; // max = 15

        System.out.println("Suma: " + suma);
        System.out.println("Producto: " + producto);
        System.out.println("Es Igual: " + esIgual);
        System.out.println("Resultado Lógico: " + resultadoLogico);
        System.out.println("Incremento: " + incremento);
        System.out.println("Decremento: " + decremento);
        System.out.println("Maximo: " + max);
    }
}
```

### Conclusión

Los operadores y expresiones en Java son fundamentales para realizar cálculos, tomar decisiones y manipular datos en el código. Comprender cómo funcionan estos operadores y cómo combinarlos en expresiones es crucial para escribir programas eficientes y correctos. 

### Consideraciones Adicionales

- **Precedencia de Operadores:** Es importante conocer la precedencia y la asociatividad de los operadores para evitar errores de lógica en las expresiones.
- **Casting y Conversiones:** Asegúrate de realizar las conversiones de tipo adecuadas para evitar pérdidas de datos o errores de tipo.
- **Uso de Operadores Lógicos:** Los operadores lógicos son útiles para combinar varias condiciones en estructuras de control, pero deben usarse con cuidado para mantener la claridad del código.
