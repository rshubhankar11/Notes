# Custom HashMap Implementation in Java

Below is a simplified custom implementation of a HashMap in Java:

```java
import java.util.ArrayList;
import java.util.List;

class Entry<K, V> {
    K key;
    V value;

    public Entry(K key, V value) {
        this.key = key;
        this.value = value;
    }
}

public class CustomHashMap<K, V> {
    private static final int DEFAULT_CAPACITY = 16;
    private static final double LOAD_FACTOR = 0.75;

    private List<Entry<K, V>>[] buckets;
    private int size;

    public CustomHashMap() {
        this(DEFAULT_CAPACITY);
    }

    public CustomHashMap(int initialCapacity) {
        this.buckets = new ArrayList[initialCapacity];
        this.size = 0;
    }

    public void put(K key, V value) {
        if (key == null) {
            throw new IllegalArgumentException("Key cannot be null.");
        }

        int index = getIndex(key);
        if (buckets[index] == null) {
            buckets[index] = new ArrayList<>();
        }

        List<Entry<K, V>> bucket = buckets[index];
        for (Entry<K, V> entry : bucket) {
            if (entry.key.equals(key)) {
                entry.value = value;
                return;
            }
        }

        bucket.add(new Entry<>(key, value));
        size++;

        // Check if resizing is needed
        if ((double) size / buckets.length > LOAD_FACTOR) {
            resize();
        }
    }

    public V get(K key) {
        if (key == null) {
            throw new IllegalArgumentException("Key cannot be null.");
        }

        int index = getIndex(key);
        List<Entry<K, V>> bucket = buckets[index];
        if (bucket != null) {
            for (Entry<K, V> entry : bucket) {
                if (entry.key.equals(key)) {
                    return entry.value;
                }
            }
        }
        return null;
    }

    public void remove(K key) {
        if (key == null) {
            throw new IllegalArgumentException("Key cannot be null.");
        }

        int index = getIndex(key);
        List<Entry<K, V>> bucket = buckets[index];
        if (bucket != null) {
            for (Entry<K, V> entry : bucket) {
                if (entry.key.equals(key)) {
                    bucket.remove(entry);
                    size--;
                    return;
                }
            }
        }
    }

    public int size() {
        return size;
    }

    private int getIndex(K key) {
        return key.hashCode() % buckets.length;
    }

    private void resize() {
        int newCapacity = buckets.length * 2;
        List<Entry<K, V>>[] newBuckets = new ArrayList[newCapacity];

        for (List<Entry<K, V>> bucket : buckets) {
            if (bucket != null) {
                for (Entry<K, V> entry : bucket) {
                    int index = entry.key.hashCode() % newCapacity;
                    if (newBuckets[index] == null) {
                        newBuckets[index] = new ArrayList<>();
                    }
                    newBuckets[index].add(entry);
                }
            }
        }

        buckets = newBuckets;
    }

    public static void main(String[] args) {
        CustomHashMap<String, Integer> map = new CustomHashMap<>();

        map.put("one", 1);
        map.put("two", 2);
        map.put("three", 3);

        System.out.println("Value for 'one': " + map.get("one"));
        System.out.println("Value for 'two': " + map.get("two"));

        map.remove("two");
        System.out.println("Value for 'two' after removal: " + map.get("two"));

        System.out.println("Current size of the map: " + map.size());
    }
}
```
