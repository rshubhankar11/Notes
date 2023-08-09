# Method Overloading and Method Overriding in Java

## Method Overloading

Method overloading allows you to define multiple methods in a class with the same name but different parameter lists. The methods must have a different number or type of parameters. Java determines which method to call based on the arguments you pass when invoking the method.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

In this example, the `Calculator` class has two `add` methods with different parameter types (int and double), enabling you to use either integers or doubles for addition.

## Method Overriding

Method overriding occurs when a subclass provides a specific implementation for a method that is already defined in its superclass. The method in the subclass must have the same name, return type, and parameters as the method in the superclass.

```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow");
    }
}
```

In this example, the `Cat` class overrides the `makeSound` method from the `Animal` class to provide a different implementation that outputs "Meow" instead of the default sound.

Remember, method overloading deals with multiple methods within the same class with different parameters, while method overriding involves providing a specific implementation of a method in a subclass that's already defined in its superclass.

## In java can we override a private and static method ?

In Java, you cannot override a `private` or `static` method in the traditional sense of method overriding. `private` methods are not accessible outside their containing class, so they can't be inherited or overridden by subclasses. `static` methods are also associated with the class itself rather than instances, so they can't be overridden either. If you define a method with the same name and parameters in a subclass, it's considered a new method, not an overridden version of the `private` or static method in the parent class.

## In java can we overload a private and static method ?

Yes, you can overload a private and static method in Java. Overloading refers to defining multiple methods in the same class with the same name but different parameter lists. Access modifiers like `private` and `static` do not affect your ability to overload methods. However, keep in mind that `private` methods can only be accessed within the same class, and `static` methods belong to the class rather than instances of the class.

# Method Overriding and Overloading with Exception in Java

## Method Overriding with Exception

In Java, when you override a method in a child class, you are allowed to throw a subclass of the exception thrown by the overridden method in the parent class. However, you are not allowed to throw a broader exception.

```java
class Parent {
    void foo() throws NullPointerException {
        // Some code that may cause NullPointerException
    }
}

class Child extends Parent {
    @Override
    void foo() throws ArrayIndexOutOfBoundsException {
        // Valid, since ArrayIndexOutOfBoundsException is a subclass of NullPointerException
    }
}
```

In this example, the `Child` class overrides the `foo` method from the `Parent` class and throws a more specific exception (`ArrayIndexOutOfBoundsException`) which is a subclass of the exception thrown by the `foo` method in the `Parent` class (`NullPointerException`).

## Method Overloading with Exception

When overloading methods, you can also change the exceptions thrown, but you cannot throw broader exceptions than what the overridden or overloaded method declares.

```java
class Calculator {
    void divide(int a, int b) throws ArithmeticException {
        // Some code that may cause ArithmeticException
    }

    void divide(double a, double b) throws IllegalArgumentException {
        // Some code that may cause IllegalArgumentException
    }
}
```

In this example, the `Calculator` class overloads the `divide` method to handle both integer and double division. Each version of the method throws a different exception, but they are not broader exceptions than what the overridden method declares.
