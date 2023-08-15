# Optional Class Java 8 :

The `Optional` class was introduced in Java 8 to handle the problem of dealing with potentially absent (null) values in a safer and more expressive way. It's a container type that either holds a non-null value or represents the absence of a value, without causing null pointer exceptions.

## **Why we need it:**

In Java, using `null` to represent the absence of a value can lead to NullPointerExceptions if not handled carefully. The `Optional` class provides a way to avoid these exceptions and encourages more robust and readable code by explicitly addressing the possibility of a value being absent.

## **Methods available in the `Optional` class:**

Here are some commonly used methods in the `Optional` class:

1. `of(value)` - Creates an `Optional` instance containing the provided non-null value.
2. `ofNullable(value)` - Creates an `Optional` instance containing the provided value if it's not null; otherwise, creates an empty `Optional`.
3. `empty()` - Creates an empty `Optional` instance.
4. `isPresent()` - Checks if the `Optional` contains a value.
5. `ifPresent(consumer)` - Executes the given consumer if a value is present.
6. `orElse(other)` - Returns the contained value if present, otherwise returns the provided default value.
7. `orElseGet(supplier)` - Returns the contained value if present, otherwise calls the provided supplier to get a value.
8. `orElseThrow(exceptionSupplier)` - Returns the contained value if present, otherwise throws an exception provided by the supplier.
9. `map(mapper)` - Applies a mapper function to the value if present and returns a new `Optional` with the mapped value.
10. `flatMap(mapper)` - Similar to `map`, but the mapper function returns an `Optional` itself, and the final result is flattened.
11. `filter(predicate)` - If a value is present and satisfies the given predicate, returns the `Optional`; otherwise, returns an empty `Optional`.

**Example:**

Let's say we have a method that returns an `Optional` of a person's name:

```java
import java.util.Optional;

public class OptionalExample {
    public static Optional<String> findPersonName(int id) {
        // Simulate a database lookup
        if (id == 1) {
            return Optional.of("John Doe");
        } else {
            return Optional.empty();
        }
    }

    public static void main(String[] args) {
        int personId = 1;
        Optional<String> nameOptional = findPersonName(personId);

        if (nameOptional.isPresent()) {
            System.out.println("Person's name: " + nameOptional.get());
        } else {
            System.out.println("Person's name not found.");
        }
    }
}
```

In this example, `findPersonName` returns an `Optional` containing a person's name if the ID is 1, or an empty `Optional` otherwise. The `main` method demonstrates how to work with `Optional`: using `isPresent` to check for a value and `get` to retrieve the value. However, it's often better to use `ifPresent` or other methods provided by `Optional` to avoid direct interaction with `null` values.

Remember that the primary goal of `Optional` is to provide a more structured way to handle potentially absent values and promote code safety and readability.
