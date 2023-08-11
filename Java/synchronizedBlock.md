# `synchronized` Block in Java

The `synchronized` block in Java is used to create a critical section, ensuring that only one thread can access the enclosed code block at a time. This is especially useful when dealing with shared resources to prevent data corruption due to concurrent access.

## Why Use `synchronized` Blocks?

Concurrency issues can arise when multiple threads access shared resources simultaneously, leading to race conditions and data inconsistency. Using `synchronized` blocks helps prevent such issues by allowing only one thread to execute the synchronized code block at a time.

## Example of `synchronized` Block

```java
public class SynchronizedExample {
    private int sharedCount = 0;

    public void increment() {
        synchronized (this) {  // Using the instance as the monitor object
            sharedCount++;
        }
    }

    public int getSharedCount() {
        return sharedCount;
    }

    public static void main(String[] args) {
        SynchronizedExample example = new SynchronizedExample();

        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) {
                example.increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) {
                example.increment();
            }
        });

        thread1.start();
        thread2.start();

        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Shared Count: " + example.getSharedCount());
    }
}
```

In this example, the `increment` method is synchronized using the instance (`this`) as the monitor object. This ensures that only one thread can execute the `increment` method at a time, preventing concurrent updates to `sharedCount`.

Remember that while `synchronized` blocks help with thread safety, they can also introduce performance overhead. Careful consideration is needed to strike a balance between synchronization and performance optimization.
