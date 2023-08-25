# Java Errors and Exceptions

## Table of Contents

- [Introduction](#introduction)
- [Error vs. Exception](#error-vs-exception)
  - [Errors](#errors)
  - [Exceptions](#exceptions)
- [Checked vs. Unchecked Exceptions](#checked-vs-unchecked-exceptions)
  - [Checked Exceptions](#checked-exceptions)
  - [Unchecked Exceptions](#unchecked-exceptions)
- [Common Exception Classes](#common-exception-classes)
- [Exception Handling](#exception-handling)
  - [try-catch](#try-catch)
  - [try-catch-finally](#try-catch-finally)
  - [Multiple catch Blocks](#multiple-catch-blocks)
  - [Throwing Exceptions](#throwing-exceptions)
  - [Custom Exceptions](#custom-exceptions)

## Introduction

In Java, errors and exceptions are used to handle abnormal situations that can disrupt the normal flow of a program. Understanding the differences between errors and exceptions, as well as checked and unchecked exceptions, is crucial for writing reliable and robust code.

## Error vs. Exception

|                   | **Errors**                                                                                                                                                   | **Exceptions**                                                                                                                                                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Definition**    | Errors represent serious problems that typically cannot be handled by the program. They often indicate issues that are beyond the control of the programmer. | Exceptions are events that occur during the execution of a program that disrupt the normal flow of instructions. They can be handled by the programmer to prevent program crashes. |
| **Examples**      | OutOfMemoryError, StackOverflowError                                                                                                                         | NullPointerException, IllegalArgumentException                                                                                                                                     |
| **Handling**      | Usually not caught or handled in code, as they indicate critical issues.                                                                                     | Should be caught and handled to ensure graceful program execution.                                                                                                                 |
| **Inheritance**   | Extends `java.lang.Error`                                                                                                                                    | Extends `java.lang.Exception`                                                                                                                                                      |
| **Unrecoverable** | Often unrecoverable; program might terminate.                                                                                                                | Generally recoverable; program can continue after handling.                                                                                                                        |

## Checked vs. Unchecked Exceptions

|                | **Checked Exceptions**                                                                                                                               | **Unchecked Exceptions**                                                                                                     |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Definition** | Checked exceptions are exceptions that must be either caught using a try-catch block or declared using the `throws` keyword in the method signature. | Unchecked exceptions are exceptions that don't need to be caught or declared. They typically result from programming errors. |
| **Examples**   | IOException, SQLException                                                                                                                            | NullPointerException, ArrayIndexOutOfBoundsException                                                                         |
| **Handling**   | Required to be caught or declared, otherwise a compilation error occurs.                                                                             | Optional to catch or declare. Compiler doesn't enforce handling.                                                             |

## Common Exception Classes

- `NullPointerException`: Occurs when an object reference is null.
- `ArrayIndexOutOfBoundsException`: Occurs when trying to access an array element with an invalid index.
- `FileNotFoundException`: Occurs when a specified file is not found.
- `IOException`: Represents a general input/output exception.
- `NumberFormatException`: Occurs when a string cannot be parsed into a numeric value.

## Exception Handling

### try-catch

The `try-catch` block is used to catch and handle exceptions.

```java
try {
    // Code that may cause an exception
} catch (ExceptionType e) {
    // Handle the exception
}
```

### try-catch-finally

The `finally` block ensures that code is executed regardless of whether an exception occurs.

```java
try {
    // Code that may cause an exception
} catch (ExceptionType e) {
    // Handle the exception
} finally {
    // Code that always executes
}
```

### Multiple catch Blocks

Handling different exceptions with multiple catch blocks.

```java
try {
    // Code
} catch (ExceptionType1 e1) {
    // Handle e1
} catch (ExceptionType2 e2) {
    // Handle e2
}
```

### Throwing Exceptions

Throwing an exception explicitly using the `throw` keyword.

```java
if (condition) {
    throw new CustomException("This is a custom exception.");
}
```

## Custom Exceptions

Custom exceptions allow you to define your own exception classes to represent specific error scenarios in your application. These exceptions can be more meaningful and specific compared to the built-in exception classes. Here's how to create and use custom exceptions:

### Creating Custom Exception

To create a custom exception, you need to define a new class that extends an existing exception class (usually `Exception` or its subclasses).

```java
public class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}
```

### When to Use Custom Exception

Custom exceptions are useful when you want to handle specific error conditions in a more organized manner. Use them in situations where:

- The built-in exception classes don't accurately represent the error scenario.
- You want to encapsulate additional information about the exception.
- You want to provide more context to the caller of the method.

### Rules for Custom Exceptions

When creating custom exceptions, keep the following rules in mind:

1. **Inheritance**: Your custom exception should extend from the appropriate exception class (usually `Exception` or its subclasses like `RuntimeException`).
2. **Constructors**: Provide constructors to initialize the custom exception with relevant information. You can also call the parent class constructor using `super(message)`.
3. **Descriptive Names**: Give meaningful and descriptive names to your custom exceptions to clearly convey their purpose.
4. **Do Not Overcomplicate**: Avoid creating too many custom exceptions for every minor error. Focus on exceptional cases that need special handling.

### Example: Using Custom Exception

Here's an example of how to use a custom exception in a method:

```java
public class CustomExceptionExample {
    public static void main(String[] args) {
        try {
            validateAge(15);
        } catch (InvalidAgeException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }

    public static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be at least 18.");
        }
        // Other validation logic
    }
}

class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```

In this example, the custom exception `InvalidAgeException` is thrown when the age is below 18. This provides a clear indication of what went wrong and allows for targeted exception handling.

---

Feel free to integrate this section about custom exceptions into the existing Markdown content. This additional information covers the creation, usage, and guidelines for custom exceptions in Java.
