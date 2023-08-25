# Java Inheritance Concept

Inheritance is a fundamental concept in object-oriented programming (OOP) where a class inherits the properties (fields) and behaviors (methods) of another class. In Java:

- The class that is inherited from is called the **superclass** or **parent class**.
- The class that inherits from another class is called the **subclass** or **child class**.
- A subclass can extend the functionality of its superclass by adding new methods or overriding existing ones.
- The `extends` keyword is used to establish an inheritance relationship between classes.

In the example provided:

- The `Child` class extends the `Parent` class, inheriting its `house` method.
- The `Child` class overrides the `house` method to provide its own implementation.
- Polymorphism allows you to store a child object in a parent reference, and the overridden method of the child will be invoked at runtime.

## Java Inheritance Example and Notes

```java
class Parent {
    public void house() {
        System.out.println("Small House");
    }
}

class Child extends Parent {
    public void house() {
        System.out.println("Big House");
    }
}

/**
 * Inheritance Example
 */
class InheritanceExample {
    public static void main(String[] args) {
        // We can store a child object in a parent reference
        Parent p = new Child();

        // When calling the 'house' method, it is overridden in the Child class,
        // so the Child's version of 'house' will be invoked.
        p.house(); // Output: Big House

        // Attempting to assign a parent object to a child reference will result in an error
        // Child c = new Parent(); // Type mismatch error
        // Child c = (Child) new Parent(); // This casting will still lead to runtime error

        Child child = new Child();
        child.house(); // Output: Big House

        Parent parent = new Parent();
        parent.house(); // Output: Small House
    }
}
```

## Inheritance in Java: Overriding and Overloading

### Method Overriding

- **Method Overriding**: When a subclass provides a specific implementation for a method that is already defined in its superclass.
- The overriding method in the subclass must have the same name, return type, and parameters as the method in the superclass.
- The `@Override` annotation is used to indicate that a method is intended to override a method in the superclass.

### Method Overloading

- **Method Overloading**: When multiple methods in the same class have the same name but different parameter lists.
- The methods must have different parameter types or a different number of parameters.
- Overloaded methods are differentiated based on the number and types of their parameters.
- Method overloading is determined at compile time based on the reference type.

## Tricky Interview Questions on Inheritance

1. **Question**: Can a subclass access private methods of its superclass?

   - **Answer**: No, a subclass cannot directly access private methods of its superclass. Private methods are not inherited.

2. **Question**: What's the difference between method overriding and method overloading?

   - **Answer**: Method overriding involves providing a specific implementation of a method in a subclass that's already defined in its superclass. Method overloading involves having multiple methods with the same name in the same class but different parameter lists.

3. **Question**: Can you override a static method?

   - **Answer**: Yes, you can override a static method, but the overridden method in the subclass won't be called using dynamic method dispatch. Instead, the method from the superclass will be called based on the reference type.

4. **Question**: Can you override a final method?

   - **Answer**: No, you cannot override a final method. The `final` modifier on a method prevents it from being overridden by any subclasses.

5. **Question**: What is the diamond problem in inheritance, and how does Java handle it?

   - **Answer**: The diamond problem occurs when a class inherits from two classes that have a common superclass. Java resolves this by giving precedence to the most specific implementation (the class closest to the inheriting class) during method invocation.

6. **Question**: Can you override a constructor in Java?
   - **Answer**: Constructors are not inherited, so you can't override them. However, constructors in the superclass are invoked as part of the subclass's constructor using `super()`.

## Inheritance : Exception Handling

1. **Checked Exceptions**:

   - If a parent class method throws a checked exception, the overridden method in the child class can throw:
     - The same exception.
     - A subclass of the exception.
     - No exception (i.e., no `throws` clause at all).

2. **Unchecked Exceptions** (Subclasses of `RuntimeException`):

   - If a parent class method throws an unchecked exception, the overridden method in the child class can throw:
     - The same exception.
     - A subclass of the exception.
     - No exception (i.e., no `throws` clause at all).

3. **Checked Exception Subtypes**:
   - If a parent class method throws a checked exception subtype, the overridden method in the child class can:
     - Choose not to throw an exception.
     - Choose to throw the same exception or any of its subtypes.

It's important to note that the overriding method cannot throw broader (more general) exceptions than the method it overrides.

Here's an example demonstrating these rules:

```java
class Parent {
    void method() throws Exception {
        // ...
    }
}

class Child extends Parent {
    @Override
    void method() throws IOException { // Subtype of Exception
        // ...
    }
}

class AnotherChild extends Parent {
    @Override
    void method() { // No exception
        // ...
    }
}
```

In the example:

- `Child` class overrides the `method` of the `Parent` class and throws a subtype of `Exception`, which is `IOException`.
- `AnotherChild` class overrides the `method` of the `Parent` class without throwing any exception.


## Important/Tricky Interview Question:

1. **Question**: Can a subclass method throw a broader exception than the superclass method it overrides?

   - **Answer**: No, it cannot. Subclass methods can only throw exceptions that are the same as, or narrower than, the exceptions thrown by the superclass method.

2. **Question**: What happens if an overridden method throws an unchecked exception?

   - **Answer**: If the overridden method in the subclass throws an unchecked exception (subclass of `RuntimeException`), the compiler doesn't force you to declare it in the `throws` clause.

3. **Question**: What if the overridden method in the parent class doesn't declare any exceptions, but the subclass method wants to throw a checked exception?

   - **Answer**: The compiler will allow this. Subclass methods can choose not to throw any exceptions or throw narrower (subtypes of) exceptions.

4. **Question**: Can you catch a broader exception type before a narrower one?

   - **Answer**: No, if you catch a broader exception type before a narrower one in a try-catch block, it will result in a compilation error.

5. **Question**: How does Java handle exceptions in constructors and inheritance?

   - **Answer**: Constructors in subclasses can throw exceptions, but if a constructor in a subclass throws a checked exception, the corresponding constructor in the superclass must also declare that exception or a superclass of it in its `throws` clause.

6. **Question**: Can you throw multiple exceptions in a single catch block?

   - **Answer**: Yes, using multi-catch syntax (Java 7 and later). For example: `catch (IOException | SQLException e) { ... }`.

7. **Question**: What's the difference between using `throws` in a method signature and using `throw` within the method body?

   - **Answer**: `throws` is used in a method signature to declare that the method might throw a specific type of exception. `throw` is used within the method body to manually throw an exception.

8. **Question**: Can an interface method throw an exception?
   - **Answer**: Yes, an interface method can declare exceptions using the `throws` clause. However, implementing classes are not required to throw those exceptions.

