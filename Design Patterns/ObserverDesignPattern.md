# Observer Design Pattern in Java

The Observer Design Pattern is a behavioral pattern that defines a one-to-many relationship between objects. When one object (the subject) changes its state, all its dependents (observers) are notified and updated automatically.

### Example Scenario

Imagine an online store where customers subscribe to product updates. When a new product is added, all subscribed customers should receive notifications.

### Implementation Steps

1. **Define the Subject Interface**:

   - Create an interface, `Subject`, with methods for registering, removing, and notifying observers.

2. **Define the Observer Interface**:

   - Create an interface, `Observer`, with a method that gets called when the subject's state changes.

3. **Create Concrete Classes**:

   - Implement the `Subject` interface in a concrete class, e.g., `ProductPublisher`.
   - Implement the `Observer` interface in concrete classes, e.g., `Customer`.

4. **Register Observers**:

   - In the `Subject` class, maintain a list of observers.
   - Provide methods to register and remove observers.

5. **Notify Observers**:
   - When the subject's state changes, iterate through the list of observers and call their update methods.

### Example: Online Store Product Updates

```java
import java.util.ArrayList;
import java.util.List;

// Step 1: Define Subject interface
interface Subject {
    void registerObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// Step 2: Define Observer interface
interface Observer {
    void update(String productName);
}

// Step 3: Concrete classes
class ProductPublisher implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String productName;

    public void addProduct(String productName) {
        this.productName = productName;
        notifyObservers();
    }

    @Override
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(productName);
        }
    }
}

class Customer implements Observer {
    private String name;

    public Customer(String name) {
        this.name = name;
    }

    @Override
    public void update(String productName) {
        System.out.println(name + " received a notification: New product added - " + productName);
    }
}

public class ObserverPatternExample {
    public static void main(String[] args) {
        ProductPublisher publisher = new ProductPublisher();

        Customer customer1 = new Customer("Alice");
        Customer customer2 = new Customer("Bob");

        publisher.registerObserver(customer1);
        publisher.registerObserver(customer2);

        publisher.addProduct("Smartphone");
        publisher.addProduct("Laptop");
    }
}
```

### Benefits of Observer Pattern

- **Loose Coupling**: Subjects and observers are loosely coupled, allowing easy addition of new observers without modifying the subject's code.
- **Flexibility**: The subject knows only about the observer interface, so new types of observers can be added.
- **Real-time Updates**: Observers are automatically updated when the subject's state changes.

The Observer Design Pattern is useful when you need to maintain a consistent state among multiple objects and notify them about changes without tightly coupling them together.
