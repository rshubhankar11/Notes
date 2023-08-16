# Iterator Design Pattern in Java

The Iterator Design Pattern provides a way to access elements of a collection sequentially without exposing its underlying representation. It encapsulates the process of traversing through a collection's elements.

### Example Scenario

Consider a music playlist. You want to iterate through the songs in the playlist without needing to know how the songs are stored internally.

### Implementation Steps

1. **Create an Iterator Interface**: Define an `Iterator` interface with methods like `hasNext` and `next`.

2. **Create a Collection Interface**: Define a `Collection` interface with a method that returns an `Iterator`.

3. **Create Concrete Classes**: Implement the `Collection` interface in a concrete class, e.g., `Playlist`. Implement the `Iterator` interface in a concrete class, e.g., `PlaylistIterator`.

4. **Implement Iteration Logic**: In the `PlaylistIterator` class, implement the `hasNext` and `next` methods to traverse through the playlist.

### Example: Music Playlist Iterator

```java
import java.util.ArrayList;
import java.util.List;

// Step 1: Create Iterator interface
interface Iterator {
    boolean hasNext();
    Object next();
}

// Step 2: Create Collection interface
interface Collection {
    Iterator createIterator();
}

// Step 3: Concrete classes
class Song {
    private String name;

    public Song(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

class Playlist implements Collection {
    private List<Song> songs = new ArrayList<>();

    public void addSong(Song song) {
        songs.add(song);
    }

    @Override
    public Iterator createIterator() {
        return new PlaylistIterator(songs);
    }
}

class PlaylistIterator implements Iterator {
    private List<Song> songs;
    private int currentPosition = 0;

    public PlaylistIterator(List<Song> songs) {
        this.songs = songs;
    }

    @Override
    public boolean hasNext() {
        return currentPosition < songs.size();
    }

    @Override
    public Object next() {
        Song song = songs.get(currentPosition);
        currentPosition++;
        return song;
    }
}

public class IteratorPatternExample {
    public static void main(String[] args) {
        Playlist playlist = new Playlist();
        playlist.addSong(new Song("Song 1"));
        playlist.addSong(new Song("Song 2"));
        playlist.addSong(new Song("Song 3"));

        Iterator iterator = playlist.createIterator();
        while (iterator.hasNext()) {
            Song song = (Song) iterator.next();
            System.out.println("Playing: " + song.getName());
        }
    }
}
```

### Benefits of Iterator Pattern

- **Separation of Concerns**: The client code is decoupled from the underlying collection structure.
- **Consistent Interface**: Provides a uniform way to traverse different types of collections.
- **Single Responsibility**: Each class is responsible for a specific task.

### Interview Questions

1. **Question**: What is the purpose of the Iterator Design Pattern?

   - **Answer**: The Iterator Pattern provides a way to access elements of a collection sequentially without exposing its internal representation.

2. **Question**: How does the Iterator Pattern achieve loose coupling?

   - **Answer**: It encapsulates the traversal logic, so client code doesn't need to know about the internal structure of the collection.

3. **Question**: Can you give an example of a real-world scenario where the Iterator Pattern could be useful?

   - **Answer**: Iterating through database query results or a file system directory.

4. **Question**: How does the Iterator Pattern promote the "Open/Closed Principle"?

   - **Answer**: You can introduce new types of collections or iterators without modifying existing code.

5. **Question**: What's the difference between the Iterator Pattern and the enhanced for loop (`for-each` loop) in Java?

   - **Answer**: The Iterator Pattern is more flexible and allows custom iteration logic, while the enhanced for loop is simpler and suitable for basic iteration.

6. **Question**: Can the Iterator Pattern be used for any type of collection?
   - **Answer**: Yes, the Iterator Pattern can be applied to various types of collections, such as arrays, lists, trees, etc.

By understanding and practicing the Iterator Design Pattern, you'll be better prepared to manage collections in a flexible and efficient way.
