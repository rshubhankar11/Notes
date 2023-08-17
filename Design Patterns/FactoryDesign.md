# Factory Design Pattern in Java

The **Factory Design Pattern (Also called as Factory method design pattern)** is a creational design pattern that provides an interface for creating objects in a super class but allows subclasses to alter the type of objects that will be created. It provides a way to create objects without specifying the exact class of object that will be created. This pattern promotes loose coupling and follows the "Open/Closed Principle," allowing easy addition of new object types without modifying existing code.

### Why It's Needed

The Factory Design Pattern is needed for the following reasons:

- **Encapsulation:** It encapsulates object creation logic in a separate class, promoting modular and organized code.
- **Decoupling:** It decouples client code from the concrete classes, making it easier to switch between different implementations.
- **Flexibility:** It allows adding new types of objects without modifying existing code.
- **Abstraction:** It provides a level of abstraction by using a common interface for object creation.

### Use Case

A common use case for the Factory Design Pattern is in creating instances of objects where the exact class to be instantiated is determined at runtime. For example, imagine a vehicle manufacturing scenario where you have different types of vehicles: Car, Truck, and Bike.

### Example

Here's an example of how to create a Factory Design Pattern for creating different types of vehicles:

```java
// Vehicle interface
interface Vehicle {
    void drive();
}

// Concrete Vehicle implementations
class Car implements Vehicle {
    @Override
    public void drive() {
        System.out.println("Driving a car.");
    }
}

class Truck implements Vehicle {
    @Override
    public void drive() {
        System.out.println("Driving a truck.");
    }
}

class Bike implements Vehicle {
    @Override
    public void drive() {
        System.out.println("Riding a bike.");
    }
}

// VehicleFactory to create instances
class VehicleFactory {
    public Vehicle createVehicle(String type) {
        switch (type.toLowerCase()) {
            case "car":
                return new Car();
            case "truck":
                return new Truck();
            case "bike":
                return new Bike();
            default:
                throw new IllegalArgumentException("Invalid vehicle type.");
        }
    }
}
```

### Advantages

- **Flexibility:** Easy to add new concrete classes without modifying existing code.
- **Decoupling:** Client code doesn't need to know the specific concrete class being created.
- **Abstraction:** It promotes the use of interfaces and abstractions in object creation.

### Disadvantages

- **Complexity:** For a small number of classes, the Factory pattern can introduce unnecessary complexity.
- **Overhead:** Requires additional classes, which might be overkill for simple scenarios.

For further information, you can check the [Factory Design Pattern](https://refactoring.guru/design-patterns/factory-method) guide on the Refactoring Guru website.
