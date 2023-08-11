# Default Values in Java

In Java, variables are assigned default values if they are not explicitly initialized. Default values are assigned based on the data type of the variable.

## Default Values for Primitive Types

- `byte`: 0
- `short`: 0
- `int`: 0
- `long`: 0L
- `float`: 0.0f
- `double`: 0.0
- `char`: '\u0000' (null character)
- `boolean`: false

## Default Values for Wrapper Classes

- `Byte`: null
- `Short`: null
- `Integer`: null
- `Long`: null
- `Float`: null
- `Double`: null
- `Character`: null
- `Boolean`: null

## Default Values for String

- `String`: null

### Example for Primitive Types and Wrapper Classes

```java
public class DefaultValuesExample {
    public static void main(String[] args) {
        byte byteVar;
        short shortVar;
        int intVar;
        long longVar;
        float floatVar;
        double doubleVar;
        char charVar;
        boolean booleanVar;

        Byte byteObj;
        Short shortObj;
        Integer intObj;
        Long longObj;
        Float floatObj;
        Double doubleObj;
        Character charObj;
        Boolean booleanObj;

        String stringVar;

        // Default values for primitive types
        System.out.println("byte: " + byteVar);        // Output: byte: 0
        System.out.println("short: " + shortVar);      // Output: short: 0
        System.out.println("int: " + intVar);          // Output: int: 0
        System.out.println("long: " + longVar);        // Output: long: 0
        System.out.println("float: " + floatVar);      // Output: float: 0.0
        System.out.println("double: " + doubleVar);    // Output: double: 0.0
        System.out.println("char: " + charVar);        // Output: char:
        System.out.println("boolean: " + booleanVar);  // Output: boolean: false

        // Default values for wrapper classes
        System.out.println("Byte: " + byteObj);        // Output: Byte: null
        System.out.println("Short: " + shortObj);      // Output: Short: null
        System.out.println("Integer: " + intObj);      // Output: Integer: null
        System.out.println("Long: " + longObj);        // Output: Long: null
        System.out.println("Float: " + floatObj);      // Output: Float: null
        System.out.println("Double: " + doubleObj);    // Output: Double: null
        System.out.println("Character: " + charObj);   // Output: Character: null
        System.out.println("Boolean: " + booleanObj);  // Output: Boolean: null

        // Default value for String
        System.out.println("String: " + stringVar);    // Output: String: null
    }
}
```

Remember that initializing variables explicitly is a good practice to ensure predictable behavior in your code.
