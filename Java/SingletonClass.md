# Creating a Singleton Class in Java

A Singleton class in Java ensures that only one instance of the class can be created throughout the application's lifetime. To create a Singleton class, follow these steps:

1. **Private Constructor:** Make the class constructor `private` to prevent external instantiation of the class.

2. **Private Static Instance:** Create a `private static` instance of the class within the class itself.

3. **Static Method to Get Instance:** Provide a `public static` method that returns the single instance of the class. This method should be the only way to access the instance.

Here's an example of a Singleton class:

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Private constructor prevents external instantiation
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
