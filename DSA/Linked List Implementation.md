## Singly Linked List Implementation in Java

Below is a basic implementation of a singly linked list in Java:

Node Creation :

```java
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

Custom LinkedList:

```Java
class LinkedList {

     Node head;

    public LinkedList() {
        this.head = null;
    }

    // Method to insert a new node at the end of the linked list
    public void append(int data) {
        Node newNode = new Node(data);

        if (head == null) {
            head = newNode;
            return;
        }

        Node current = head;
        while (current.next != null) {
            current = current.next;
        }

        current.next = newNode;
    }

    // Method to print the linked list
    public void display() {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }
        // System.out.println("null");
    }

}

public class Main {
public static void main(String[] args) {
LinkedList myList = new LinkedList();

        myList.append(1);
        myList.append(2);
        myList.append(3);

        myList.display(); // Output: 1 -> 2 -> 3 -> null
    }

}

```

This code defines a `Node` class to represent individual elements in the linked list, a `LinkedList` class to manage the list, and a `Main` class for testing the implementation. You can add more methods as needed for various operations like insertion, deletion, searching, etc., based on your requirements.
