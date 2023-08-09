# Creating an Immutable Class in Java

An immutable class in Java is a class whose instances cannot be modified after they are created. To achieve immutability, follow these steps:

1. **Declare the class as `final`:** Make the class itself `final` to prevent subclassing, as subclasses might introduce mutability.

2. **Make fields `private` and `final`:** Declare the fields as `private` to restrict direct access and `final` to ensure they cannot be modified after initialization.

3. **Provide only getter methods:** Create getter methods for the fields to allow external access without allowing modifications.

4. **No setter methods:** Do not provide any setter methods that modify the state of the object.

5. **Constructors for initialization:** Provide constructors that initialize all the fields of the object.

6. **Defensive copying:** If your class contains mutable objects as fields, make sure to return defensive copies of those objects in the getter methods to prevent unintended modifications.

Here's an example of an immutable class:

````java
public final class ImmutablePerson {
    private final String name;
    private final int age;

    public ImmutablePerson(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
# Creating an Immutable Class in Java

An immutable class in Java is a class whose instances cannot be modified after they are created. To achieve immutability, follow these steps:

1. **Declare the class as `final`:** Make the class itself `final` to prevent subclassing, as subclasses might introduce mutability.

2. **Make fields `private` and `final`:** Declare the fields as `private` to restrict direct access and `final` to ensure they cannot be modified after initialization.

3. **Provide only getter methods:** Create getter methods for the fields to allow external access without allowing modifications.

4. **No setter methods:** Do not provide any setter methods that modify the state of the object.

5. **Constructors for initialization:** Provide constructors that initialize all the fields of the object.

6. **Defensive copying:** If your class contains mutable objects as fields, make sure to return defensive copies of those objects in the getter methods to prevent unintended modifications.

Here's an example of an immutable class:

```java
public final class ImmutablePerson {
    private final String name;
    private final int age;

    public ImmutablePerson(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
````
