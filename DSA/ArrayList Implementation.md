# Custom ArrayList Implementation in Java

Below is a simplified custom implementation of an ArrayList in Java:

```java
import java.util.Arrays;

public class CustomArrayList<T> {
    private static final int DEFAULT_CAPACITY = 10;
    private Object[] array;
    private int size;

    public CustomArrayList() {
        this.array = new Object[DEFAULT_CAPACITY];
        this.size = 0;
    }

    public CustomArrayList(int initialCapacity) {
        if (initialCapacity < 0) {
            throw new IllegalArgumentException("Initial capacity cannot be negative");
        }
        this.array = new Object[initialCapacity];
        this.size = 0;
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void add(T element) {
        ensureCapacity();
        array[size++] = element;
    }

    public T get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index out of bounds: " + index);
        }
        return (T) array[index];
    }

    public void remove(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index out of bounds: " + index);
        }
        // Shift elements to the left to fill the gap
        for (int i = index; i < size - 1; i++) {
            array[i] = array[i + 1];
        }
        array[--size] = null; // Set the last element to null and decrease size
    }

    private void ensureCapacity() {
        if (size == array.length) {
            int newCapacity = array.length * 2;
            array = Arrays.copyOf(array, newCapacity);
        }
    }

    @Override
    public String toString() {
        if (size == 0) {
            return "[]";
        }
        StringBuilder builder = new StringBuilder("[");
        for (int i = 0; i < size - 1; i++) {
            builder.append(array[i]).append(", ");
        }
        builder.append(array[size - 1]).append("]");
        return builder.toString();
    }

    public static void main(String[] args) {
        CustomArrayList<Integer> list = new CustomArrayList<>();

        list.add(1);
        list.add(2);
        list.add(3);

        System.out.println("List: " + list);

        list.remove(1);

        System.out.println("List after removing element at index 1: " + list);
    }
}
```
