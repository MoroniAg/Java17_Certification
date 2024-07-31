## Clases Wrapper en Java: Detalles Completos y Métodos

### ¿Qué son las Clases Wrapper?

Las clases Wrapper en Java encapsulan tipos de datos primitivos en objetos. Esto permite tratar los tipos primitivos como objetos, lo cual es útil en situaciones que requieren objetos, como al trabajar con colecciones (`ArrayList`, `HashMap`, etc.). Las clases Wrapper proporcionan métodos útiles para manipular, convertir y comparar valores primitivos.

### Tipos de Clases Wrapper y sus Correspondientes Tipos Primitivos

1. **byte**: `Byte`
2. **short**: `Short`
3. **int**: `Integer`
4. **long**: `Long`
5. **float**: `Float`
6. **double**: `Double`
7. **char**: `Character`
8. **boolean**: `Boolean`

### Detalles y Métodos de Cada Clase Wrapper

#### 1. `Byte`

Encapsula un valor primitivo de tipo `byte` en un objeto.

**Constructores:**
- `Byte(byte value)`
- `Byte(String s)`

**Métodos:**
- `byteValue()`: Devuelve el valor `byte`.
- `compareTo(Byte anotherByte)`: Compara dos objetos `Byte`.
- `parseByte(String s)`: Convierte un `String` a `byte`.
- `toString()`: Devuelve una representación de `String` del valor `byte`.
- `valueOf(String s)`: Devuelve un objeto `Byte` que contiene el valor especificado.

**Ejemplo:**

```java
Byte byteObj = Byte.valueOf("10");
byte byteValue = byteObj.byteValue();
```

#### 2. `Short`

Encapsula un valor primitivo de tipo `short` en un objeto.

**Constructores:**
- `Short(short value)`
- `Short(String s)`

**Métodos:**
- `shortValue()`: Devuelve el valor `short`.
- `compareTo(Short anotherShort)`: Compara dos objetos `Short`.
- `parseShort(String s)`: Convierte un `String` a `short`.
- `toString()`: Devuelve una representación de `String` del valor `short`.
- `valueOf(String s)`: Devuelve un objeto `Short` que contiene el valor especificado.

**Ejemplo:**

```java
Short shortObj = Short.valueOf("1000");
short shortValue = shortObj.shortValue();
```

#### 3. `Integer`

Encapsula un valor primitivo de tipo `int` en un objeto.

**Constructores:**
- `Integer(int value)`
- `Integer(String s)`

**Métodos:**
- `intValue()`: Devuelve el valor `int`.
- `compareTo(Integer anotherInteger)`: Compara dos objetos `Integer`.
- `parseInt(String s)`: Convierte un `String` a `int`.
- `toString()`: Devuelve una representación de `String` del valor `int`.
- `valueOf(String s)`: Devuelve un objeto `Integer` que contiene el valor especificado.

**Ejemplo:**

```java
Integer intObj = Integer.valueOf("1234");
int intValue = intObj.intValue();
```

#### 4. `Long`

Encapsula un valor primitivo de tipo `long` en un objeto.

**Constructores:**
- `Long(long value)`
- `Long(String s)`

**Métodos:**
- `longValue()`: Devuelve el valor `long`.
- `compareTo(Long anotherLong)`: Compara dos objetos `Long`.
- `parseLong(String s)`: Convierte un `String` a `long`.
- `toString()`: Devuelve una representación de `String` del valor `long`.
- `valueOf(String s)`: Devuelve un objeto `Long` que contiene el valor especificado.

**Ejemplo:**

```java
Long longObj = Long.valueOf("123456789");
long longValue = longObj.longValue();
```

#### 5. `Float`

Encapsula un valor primitivo de tipo `float` en un objeto.

**Constructores:**
- `Float(float value)`
- `Float(String s)`

**Métodos:**
- `floatValue()`: Devuelve el valor `float`.
- `compareTo(Float anotherFloat)`: Compara dos objetos `Float`.
- `parseFloat(String s)`: Convierte un `String` a `float`.
- `toString()`: Devuelve una representación de `String` del valor `float`.
- `valueOf(String s)`: Devuelve un objeto `Float` que contiene el valor especificado.

**Ejemplo:**

```java
Float floatObj = Float.valueOf("12.34");
float floatValue = floatObj.floatValue();
```

#### 6. `Double`

Encapsula un valor primitivo de tipo `double` en un objeto.

**Constructores:**
- `Double(double value)`
- `Double(String s)`

**Métodos:**
- `doubleValue()`: Devuelve el valor `double`.
- `compareTo(Double anotherDouble)`: Compara dos objetos `Double`.
- `parseDouble(String s)`: Convierte un `String` a `double`.
- `toString()`: Devuelve una representación de `String` del valor `double`.
- `valueOf(String s)`: Devuelve un objeto `Double` que contiene el valor especificado.

**Ejemplo:**

```java
Double doubleObj = Double.valueOf("123.456");
double doubleValue = doubleObj.doubleValue();
```

#### 7. `Character`

Encapsula un valor primitivo de tipo `char` en un objeto.

**Constructor:**
- `Character(char value)`

**Métodos:**
- `charValue()`: Devuelve el valor `char`.
- `compareTo(Character anotherCharacter)`: Compara dos objetos `Character`.
- `toString()`: Devuelve una representación de `String` del valor `char`.
- `valueOf(char c)`: Devuelve un objeto `Character` que contiene el valor especificado.

**Ejemplo:**

```java
Character charObj = Character.valueOf('A');
char charValue = charObj.charValue();
```

#### 8. `Boolean`

Encapsula un valor primitivo de tipo `boolean` en un objeto.

**Constructores:**
- `Boolean(boolean value)`
- `Boolean(String s)`

**Métodos:**
- `booleanValue()`: Devuelve el valor `boolean`.
- `compareTo(Boolean anotherBoolean)`: Compara dos objetos `Boolean`.
- `parseBoolean(String s)`: Convierte un `String` a `boolean`.
- `toString()`: Devuelve una representación de `String` del valor `boolean`.
- `valueOf(String s)`: Devuelve un objeto `Boolean` que contiene el valor especificado.

**Ejemplo:**

```java
Boolean booleanObj = Boolean.valueOf("true");
boolean booleanValue = booleanObj.booleanValue();
```

### Detalles Adicionales y Ejemplos

**Uso en Colecciones Genéricas**

Las colecciones genéricas en Java, como `ArrayList` y `HashMap`, requieren objetos en lugar de tipos primitivos. Las clases Wrapper permiten almacenar y manipular tipos primitivos en estas colecciones.

```java
ArrayList<Integer> listaNumeros = new ArrayList<>();
listaNumeros.add(5); // Autoboxing convierte el int 5 en un Integer
int valor = listaNumeros.get(0); // Unboxing convierte el Integer a int
```

**Autoboxing y Unboxing**

El autoboxing es la conversión automática de un tipo primitivo a su clase Wrapper correspondiente, mientras que el unboxing es la conversión automática de una clase Wrapper a su tipo primitivo correspondiente.

```java
Integer a = 10; // Autoboxing convierte el int 10 en un Integer
int b = a; // Unboxing convierte el Integer a int
```

**Conversión entre Tipos Primitivos y Strings**

Las clases Wrapper proporcionan métodos para convertir entre tipos primitivos y `String`.

```java
int numero = 42;
String strNumero = Integer.toString(numero); // Convierte int a String

String strDouble = "3.14";
double doubleValue = Double.parseDouble(strDouble); // Convierte String a double
```

### Conclusión y Consideraciones Adicionales

Las clases Wrapper son esenciales para trabajar con colecciones genéricas, manipular datos y aprovechar métodos utilitarios que facilitan la conversión y comparación de tipos de datos. Comprender cómo y cuándo usar estas clases es crucial para escribir código más flexible y robusto. Además, dominar el uso de autoboxing y unboxing puede simplificar considerablemente el código, aunque es importante ser consciente de los posibles costos de rendimiento asociados con el uso excesivo de objetos en lugar de tipos primitivos.