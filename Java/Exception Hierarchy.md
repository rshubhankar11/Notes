# Java Exception Hierarchy

In Java, the exception hierarchy is represented by the `java.lang.Exception` class, which serves as the root class for most Java exceptions. There are two main branches in the exception hierarchy: checked exceptions and unchecked exceptions.

## Checked Exceptions

Checked exceptions are exceptions that are checked at compile-time. Any method that might throw a checked exception must declare it using a `throws` clause or handle it using a `try-catch` block. Examples of checked exceptions include:

- `IOException`
- `SQLException`
- `ClassNotFoundException`

All checked exceptions extend directly from the `java.lang.Exception` class but do not extend the `RuntimeException` class.

## Unchecked Exceptions

Unchecked exceptions are not checked at compile-time, so there's no requirement to handle or declare them. These exceptions occur due to programming errors or issues that the programmer could have avoided. They are subclasses of `RuntimeException`. Examples of unchecked exceptions include:

- `NullPointerException`
- `ArrayIndexOutOfBoundsException`
- `ArithmeticException`
- `IllegalArgumentException`

### Exception Hierarchy Representation:

```java
Throwable
├── Error
│   ├── VirtualMachineError
│   │   ├── StackOverflowError
│   │   └── OutOfMemoryError
│   └── ...
└── Exception
    ├── RuntimeException
    │   ├── NullPointerException
    │   ├── IllegalArgumentException
    │   └── ...
    └── IOException
        ├── FileNotFoundException
        ├── EOFException
        └── ...
```

- Throwable is the root class for all exceptions and errors in Java.
- Error represents serious problems that are usually beyond the control of the application and should not be caught or handled by regular code.
- Exception is the superclass for all exceptions that are not considered errors.
- RuntimeException is a subclass of Exception and includes exceptions that are unchecked (do not need to be explicitly caught or declared).
