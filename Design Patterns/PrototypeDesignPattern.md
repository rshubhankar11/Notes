# **Prototype Design Pattern:**

The Prototype design pattern is a creational pattern that focuses on creating copies of objects, known as prototypes, instead of creating new instances from scratch. It involves cloning existing objects and customizing them as needed. This pattern is especially useful when creating new instances is resource-intensive or when objects have complex initialization processes.

## **Where to Use:**

Use the Prototype pattern when:

1. Creating instances of a class is time-consuming or resource-intensive.
2. Objects have many shared characteristics, and most of the properties remain the same across instances.
3. You want to avoid subclassing just to create slight variations of objects.

## **Why Use:**

The Prototype pattern provides the following benefits:

1. **Efficient Object Creation:** It reduces the overhead of creating objects by cloning existing ones, which can be faster than creating new instances from scratch.

2. **Customization:** You can easily create variations of objects by cloning and modifying their properties.

3. **Reduced Subclassing:** Instead of creating subclasses for each variation, you can clone and customize prototypes, reducing the need for complex class hierarchies.

## **Steps to Create Prototype Design Pattern:**

1. **Define Prototype Interface or Abstract Class:** Declare methods for cloning an object.

2. **Create Concrete Prototype Classes:** Implement the prototype interface and provide concrete implementations of the clone method.

3. **Create a Prototype Manager (Optional):** Optionally, you can create a manager class to store and manage a collection of prototypes.

**Example:**

Let's create an example of a `Shape` prototype. We'll have different shapes like `Circle` and `Rectangle`, and we'll create a prototype manager to store and manage the prototypes.

```java
import java.util.HashMap;
import java.util.Map;

interface Shape extends Cloneable {
    Shape clone();
    void draw();
}

class Circle implements Shape {
    @Override
    public Shape clone() {
        return new Circle();
    }

    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

class Rectangle implements Shape {
    @Override
    public Shape clone() {
        return new Rectangle();
    }

    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

class PrototypeManager {
    private Map<String, Shape> shapeMap = new HashMap<>();

    public void registerShape(String key, Shape shape) {
        shapeMap.put(key, shape);
    }

    public Shape getShape(String key) {
        return shapeMap.get(key).clone();
    }
}

public class PrototypeExample {
    public static void main(String[] args) {
        PrototypeManager manager = new PrototypeManager();

        Shape circlePrototype = new Circle();
        Shape rectanglePrototype = new Rectangle();

        manager.registerShape("circle", circlePrototype);
        manager.registerShape("rectangle", rectanglePrototype);

        Shape clonedCircle = manager.getShape("circle");
        Shape clonedRectangle = manager.getShape("rectangle");

        clonedCircle.draw();
        clonedRectangle.draw();
    }
}
```

In this example, the `Shape` interface declares the `clone` method, and `Circle` and `Rectangle` classes implement it to provide cloned instances. The `PrototypeManager` class manages the prototypes and provides methods to register and retrieve them.

When you run the example, it clones the prototypes using the manager and demonstrates that you can create instances of different shapes without creating new instances from scratch.

Remember, the Prototype pattern shines when creating object copies is resource-intensive or complex. It allows you to create variations efficiently by cloning and customizing existing objects.

## Example of Prototype Design pattern implementing Deep Copy:

Here is an example of the Prototype design pattern using deep copy in Java. We'll use a similar scenario as before, but this time we'll ensure that the deep copy creates new instances of nested objects.

```java
class Address implements Cloneable {
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

    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();
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
        Address clonedAddress = (Address) address.clone(); // Deep copy the Address object
        return new Person(name, clonedAddress); // Create a new Person object with the cloned Address
    }

    public String getName() {
        return name;
    }

    public Address getAddress() {
        return address;
    }
}

public class DeepPrototypeExample {
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

In this example, the `Address` class implements the `Cloneable` interface, and its `clone` method performs a shallow copy. However, when we clone the `Person` object, we create a new `Address` object using its `clone` method, which effectively performs a deep copy of the `Address` object. This ensures that the copied person's address is a new independent object with its own memory space.

Running the example will show that the original and copied cities are different, illustrating the independence of the two objects.
