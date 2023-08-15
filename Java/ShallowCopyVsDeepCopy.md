# Shallow Copy Vs Deep Copy :

## **Shallow Copy:**

A shallow copy is a type of object copying where the new object is created, and its fields are assigned the values of the fields in the original object. However, if the original object contains references to other objects (such as fields pointing to other objects), the shallow copy will copy these references, not the actual objects they point to. As a result, both the original object and the copy will share references to the same objects, leading to potential problems.

## **Problem with Shallow Copy:**

The main problem with shallow copying arises when you have mutable objects (objects whose state can be changed) as fields within the original object. Since the shallow copy merely copies references to these mutable objects, any changes made to the mutable objects within the copy will also reflect in the original object, and vice versa. This can lead to unexpected behavior and data corruption.

**Example:**

Let's consider an example using Java's cloning mechanism to demonstrate the problem with shallow copy.

```java
class Address {
    private String city;

    public Address(String city) {
        this.city = city;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }
}

class Person implements Cloneable {
    private String name;
    private Address address;

    public Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    public String getName() {
        return name;
    }

    public Address getAddress() {
        return address;
    }
}

public class ShallowCopyExample {
    public static void main(String[] args) {
        Address originalAddress = new Address("City1");
        Person originalPerson = new Person("John", originalAddress);

        try {
            Person copiedPerson = (Person) originalPerson.clone();
            copiedPerson.getAddress().setCity("City2");

            System.out.println("Original City: " + originalPerson.getAddress().getCity());
            System.out.println("Copied City: " + copiedPerson.getAddress().getCity());
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, the `Person` class has a reference to the `Address` class. When we create a shallow copy of the `Person` object and modify the city of the copied person's address, the original person's address is also modified. This is because both the original and the copied person share the same reference to the `Address` object.

The output will show that both the original and copied city are "City2," even though we only explicitly modified the copied person's address.

This demonstrates the problem with shallow copying when mutable objects are involved. If you need independent copies of mutable objects, you need to perform a deep copy, which involves copying the mutable objects themselves rather than just their references.

## **Deep Copy:**

A deep copy is a type of object copying where a new object is created, and all of its fields, including fields that reference other objects, are copied as well. This results in a completely independent copy of the original object and all the objects it references.

## **Why Use Deep Copy:**

Deep copying is useful when you want to create a new object that is entirely separate from the original, including its nested objects. This prevents unintended sharing of mutable objects between the original and the copy, which can lead to unexpected behavior and data integrity issues.

## **Example of Deep Copy using Cloning in Java:**

Example to create a new `Address` object instead of cloning it using the `Cloneable` interface.

```java
class Address {
    private String city;

    public Address(String city) {
        this.city = city;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }
}

class Person implements Cloneable {
    private String name;
    private Address address;

    public Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    @Override
    public Object clone() throws CloneNotSupportedException {
        Address clonedAddress = new Address(address.getCity()); // Create a new Address object
        return new Person(name, clonedAddress); // Create a new Person object with the cloned Address
    }

    public String getName() {
        return name;
    }

    public Address getAddress() {
        return address;
    }
}

public class DeepCopyExample {
    public static void main(String[] args) {
        Address originalAddress = new Address("City1");
        Person originalPerson = new Person("John", originalAddress);

        try {
            Person copiedPerson = (Person) originalPerson.clone();
            copiedPerson.getAddress().setCity("City2");

            System.out.println("Original City: " + originalPerson.getAddress().getCity());
            System.out.println("Copied City: " + copiedPerson.getAddress().getCity());
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, instead of using the `Cloneable` interface for deep copying, we create a new `Address` object with the same city value and then create a new `Person` object with the cloned `Address` object. This achieves the same result as deep copying – the original and copied objects have separate `Address` instances.

Again, the output will show that the original and copied cities are different, demonstrating the independence of the two objects.

## Shallow Copy Vs Deep Copy Table :

| Aspect         | Shallow Copy                                    | Deep Copy                                             |
| -------------- | ----------------------------------------------- | ----------------------------------------------------- |
| Copies         | Creates a new object, but shares nested objects | Creates a new object and new copies of nested objects |
| Independence   | Objects share references to nested objects      | Objects have independent copies of nested objects     |
| Complexity     | Less complex, as it copies references only      | More complex, as it copies entire object hierarchies  |
| Resource Usage | Consumes less memory due to shared references   | Consumes more memory due to independent copies        |
| Modifications  | Changes to nested objects affect both copies    | Changes to nested objects don't affect each other     |
| Use Cases      | Suitable when shared state is acceptable        | Suitable when each copy should be fully independent   |
| Common Usage   | Copying immutable objects, simple structures    | Copying mutable objects, complex structures           |
