# Java Records

In Java, a record is a new feature introduced in Java 16 (as of my last knowledge update in September 2021) to simplify the creation of classes for the sole purpose of holding and representing data. Records are designed to reduce the boilerplate code typically associated with creating classes that have fields, constructors, getters, equals(), hashCode(), and toString() methods. They are often used for creating immutable data objects.

## Declaration Syntax

Records are declared using the `record` keyword, followed by the name of the record and a parameter list in parentheses. The parameter list defines the components (fields) of the record. For example:

```java
record Person(String name, int age) {
}
```

## Automatically Generated Methods

When you declare a record, the Java compiler automatically generates several methods for you, including:

- A constructor that initializes the fields.
- Getter methods for each field.
- `equals()`, `hashCode()`, and `toString()` methods based on the fields.

You can still customize these methods if needed.

## Immutability

Records are typically designed to be immutable, which means their fields are final and cannot be modified after object creation. This immutability is enforced by the generated constructor, and there are no setter methods.

## Compact Syntax

Records have a concise syntax, making them more readable and reducing boilerplate code. This makes them well-suited for classes whose primary purpose is to hold data.

## Usage Examples

Records are useful for creating data-centric classes. Here's an example of using the `Person` record:

```java
Person person = new Person("Alice", 30);
System.out.println(person.name()); // Accessing the 'name' field using the auto-generated getter
System.out.println(person.age());  // Accessing the 'age' field using the auto-generated getter
System.out.println(person);        // Automatically uses the toString() method
```

## Custom Methods

While records automatically generate many methods, you can still add your own custom methods, which can be useful for adding behavior to your data classes.

## Compatibility

Records are fully compatible with existing Java code. You can use them alongside regular classes and interfaces.

## Limitations

Records have some limitations. For example, you cannot extend other classes when defining a record, as records implicitly extend the `java.lang.Record` class. Also, you cannot declare instance variables (fields) in a record, as all fields are implicitly final.
