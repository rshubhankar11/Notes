# Custom Set Implementation in Java

Below is a simplified custom implementation of a Set in Java using an ArrayList:

```java
import java.util.ArrayList;
import java.util.List;

public class CustomSet<T> {
    private List<T> elements;

    public CustomSet() {
        elements = new ArrayList<>();
    }

    public boolean add(T element) {
        if (!contains(element)) {
            elements.add(element);
            return true;
        }
        return false;
    }

    public boolean remove(T element) {
        return elements.remove(element);
    }

    public boolean contains(T element) {
        return elements.contains(element);
    }

    public int size() {
        return elements.size();
    }

    public boolean isEmpty() {
        return elements.isEmpty();
    }

    @Override
    public String toString() {
        return elements.toString();
    }

    public static void main(String[] args) {
        CustomSet<Integer> customSet = new CustomSet<>();

        customSet.add(1);
        customSet.add(2);
        customSet.add(3);
        customSet.add(2); // Adding a duplicate element, should not be added

        System.out.println("CustomSet: " + customSet);

        customSet.remove(2);

        System.out.println("CustomSet after removing 2: " + customSet);

        System.out.println("Contains 3: " + customSet.contains(3));
        System.out.println("Contains 2: " + customSet.contains(2));

        System.out.println("Size of CustomSet: " + customSet.size());
        System.out.println("Is CustomSet empty? " + customSet.isEmpty());
    }
}
```
