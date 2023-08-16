# ` Serialization` and `Externalization `

# What is Serialization

Serialization is the process of converting a Java object into a static stream (sequence) of bytes, which can then be saved to a database or transferred over a network.

- Classes that are eligible for serialization need to implement a special marker interface, `Serializable`. The JVM grants special privileges to the class that implements the `Serializable` interface.

- Byte stream is platform-independent. This means that once you have a stream of bytes, you can convert it into an object and run it on any kind of environment.

- For a class to be serialized successfully, two conditions must be met:

  - The class must implement the `java.io.Serializable` interface.
  - All fields in the class must be serializable. If a field is not serializable, it must be marked as `transient`.

- Static fields belong to a class (as opposed to an object) and are not serialized.

Certainly! Here's the text you provided in Markdown format:

## Serialization

- Serialization is the process of converting an object into a stream of bytes.
- To achieve this, Java provides the `ObjectOutputStream` class, which includes the `writeObject` method.

- Deserialization is the reverse process: converting a stream of bytes back into an object.
- For deserialization, Java provides the `ObjectInputStream` class, which includes the `readObject` method.

Example:

```java
FileOutputStream fileOut = new FileOutputStream("/tmp/employee.ser");
ObjectOutputStream out = new ObjectOutputStream(fileOut);
out.writeObject(e);
out.close();
fileOut.close();
```

In Markdown, code blocks can be created by surrounding the code with triple backticks (```).

Certainly! Here's the information you requested in Markdown format:

## Transient in Serialization

In Java, serialization is the process of converting an object into a byte stream to store it in memory or transfer it over the network. The `transient` keyword is used to indicate that a field should not be serialized.

### Usage of `transient`

When a field is marked as `transient`, it will be excluded from the serialization process. This is useful for fields that contain sensitive or temporary data that doesn't need to be persisted. Here's how you can use the `transient` keyword:

```java
import java.io.Serializable;

public class Person implements Serializable {
    private String name;
    private transient int age; // This field will not be serialized

    // Constructor, getters, setters, etc.
}
```

### Example

```java
import java.io.*;

public class SerializationExample {
    public static void main(String[] args) {
        // Serialization
        Person person = new Person("Alice", 30);
        try {
            FileOutputStream fileOut = new FileOutputStream("person.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(person);
            out.close();
            fileOut.close();
            System.out.println("Person object has been serialized.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialization
        try {
            FileInputStream fileIn = new FileInputStream("person.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            Person deserializedPerson = (Person) in.readObject();
            in.close();
            fileIn.close();
            System.out.println("Person object has been deserialized.");
            System.out.println("Name: " + deserializedPerson.getName());
            System.out.println("Age: " + deserializedPerson.getAge()); // Age will be 0
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, the `age` field is marked as `transient`, so when the `Person` object is deserialized, the `age` field will have its default value (0 for `int`). This demonstrates how the `transient` keyword prevents certain fields from being serialized and deserialized.

## What is Deserialization

Deserialization is the process that is the opposite of serialization. When deserializing, you begin with a byte stream and reconstruct the object you previously serialized, restoring it to its original state. However, it's crucial to have the object's definition available to recreate it successfully.

```java
FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
ObjectInputStream in = new ObjectInputStream(fileIn);
e = (Employee) in.readObject();
in.close();
fileIn.close();
```

## What is Serial Version UID

- The Java Virtual Machine (JVM) assigns a version number (long) to each serializable class. The `serialVersionUID` attribute is used to keep track of versions for a Serializable class, ensuring compatibility between a loaded class and a serialized object.

- Most Integrated Development Environments (IDEs) can generate this number automatically. It's derived from the class name, attributes, and related access modifiers. Any changes will result in a different number, potentially causing an `InvalidClassException`.

- If a serializable class doesn't explicitly declare a `serialVersionUID`, the JVM will generate one at runtime. However, it's highly recommended that each class defines its own `serialVersionUID`, as the automatically generated value can be compiler-dependent and lead to unexpected `InvalidClassExceptions`.

## How does Java Serialization work?

Java serialization operates by utilizing reflection to extract all the required data from an object's fields, including private and final fields. If a field holds an object, that object is serialized in a recursive manner. Interestingly, even if an object has getters and setters, these methods are not employed during the process of serializing an object in Java.

## How does Java deserialization work?

When deserializing a byte stream back to an object it does not use the constructor. It simply creates an empty object and uses reflection to write the data to the fields. Just like with serialization, private and final fields are also included

## Example

```java
import java.io.*;

class Person implements Serializable {
    private static final long serialVersionUID = 123456789L; // Unique serialVersionUID

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        Person person = new Person("John", 30);

        // Serialize the object
        try {
            FileOutputStream fileOut = new FileOutputStream("person.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(person);
            out.close();
            fileOut.close();
            System.out.println("Serialized data is saved in person.ser");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialize the object
        Person deserializedPerson = null;
        try {
            FileInputStream fileIn = new FileInputStream("person.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            deserializedPerson = (Person) in.readObject();
            in.close();
            fileIn.close();
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }

        if (deserializedPerson != null) {
            System.out.println("Deserialized Person:");
            System.out.println("Name: " + deserializedPerson.getName());
            System.out.println("Age: " + deserializedPerson.getAge());
        }
    }
}
```

In this example, we create a `Person` class that implements the `Serializable` interface and includes a `serialVersionUID` field to provide version control. We serialize a `Person` object to a file named "person.ser" and then deserialize it back, printing out the deserialized person's information.

Please make sure to replace `"person.ser"` with the appropriate path where you want to save the serialized data.

# What is Externalization?

Externalization in Java is employed when you require customized control over the serialization mechanism.

- In standard serialization, the Java Virtual Machine handles the entire process of writing and reading objects. This simplifies things for programmers, as they don't need to be concerned about the intricacies of serialization. However, default serialization doesn't protect sensitive information like passwords or credentials. Additionally, what if programmers want to secure specific data during serialization?

- This is where externalization comes into play. It grants programmers full control over reading and writing objects during serialization. The Java Virtual Machine relinquishes control in favor of the application, providing complete serialization control.

- Depending on our needs, we can serialize either entire data fields or portions of data fields using the `Externalizable` interface. This approach can enhance the performance of an application.

- It's important to note that the `Externalizable` interface internally extends the `Serializable` interface. This means that any class implementing `Externalizable` must also follow the requirements of `Serializable`.

## How it works?

During the serialization process, the JVM follows these steps:

- If objects support the `Externalizable` interface, the JVM serializes objects using the `writeExternal()` method.

- If objects do not support `Externalizable` but implement `Serializable`, the JVM stores objects using `ObjectOutputStream`.

- For serializable objects, the JVM serializes only instance variables that are not declared with the `transient` keyword.

- For externalizable objects, developers have complete control over what data to serialize and what to exclude.

- The order of reads during deserialization must match the order of writes during serialization.

## What is a Java deserialize vulnerability

A Java deserialize vulnerability is a security vulnerability that occurs when a malicious user tries to insert a modified serialized object into the system in order to compromise the system or its data. Think of an arbitrary code execution vulnerability that can be triggered when deserializing a serialized object.

## Inheritance Rules with Serialization and Deserialization

Several rules apply when dealing with inheritance during serialization and deserialization:

1. If the superclass is serializable, the subclass is automatically serializable as well.

2. If a superclass is not serializable, the subclass can still be serialized.

3. Even if the superclass doesn't implement the `Serializable` interface, you can serialize subclass objects if the subclass itself implements the `Serializable` interface. This implies that to serialize subclass objects, the superclass doesn't necessarily need to be serializable. However, a specific procedure applies when serializing superclass instances in this case.

4. **Serialization and Non-Serializable Superclass:**

   - Serialization: If an instance variable inherits from a non-serializable superclass, the JVM disregards the original value of that instance variable and saves the default value to the file.

   - Deserialization: If a non-serializable superclass is present, the JVM will execute instance control flow in the superclass during deserialization.

5. **Important Points:**
   - It's recommended that both the superclass and subclass should implement the `Serializable` interface for consistency.
   - `transient` fields in a superclass are not automatically considered transient in subclasses. You need to explicitly declare them as `transient` again in the subclass if you want them to be treated as such during serialization.
   - Deserialization of a subclass involves invoking constructors not only for the subclass but also for all its non-serializable superclasses.
   - When using custom serialization methods (`writeObject` and `readObject`), you must carefully manage the serialization process for both the superclass and subclass.

## How to prevent a Java deserialize vulnerability?

- The best way to prevent a Java deserialize vulnerability is to prevent Java serialization overall. If your application doesn't accept serialized objects, it can't hurt you.

- However, if you do need to implement the 'serializable' interface due to inheritance, you can override the readObject(), as seen below, to prevent actual deserialization.

## Example :

```java
import java.io.*;

class Person implements Externalizable {
    private String name;
    private int age;

    // Mandatory public no-argument constructor
    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeObject(name); // Manually write name
        out.writeInt(age);     // Manually write age
    }

    @Override
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        name = (String) in.readObject(); // Manually read name
        age = in.readInt();             // Manually read age
    }

    @Override
    public String toString() {
        return "Name: " + name + ", Age: " + age;
    }
}

public class ExternalizationExample {
    public static void main(String[] args) {
        Person person = new Person("John", 30);

        // Serialize the object
        try {
            FileOutputStream fileOut = new FileOutputStream("person.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            person.writeExternal(out); // Call the writeExternal method
            out.close();
            fileOut.close();
            System.out.println("Serialized data is saved in person.ser");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialize the object
        Person deserializedPerson = new Person(); // Mandatory no-argument constructor
        try {
            FileInputStream fileIn = new FileInputStream("person.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            deserializedPerson.readExternal(in); // Call the readExternal method
            in.close();
            fileIn.close();
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }

        System.out.println("Deserialized Person: " + deserializedPerson);
    }
}
```

In this example, we define a `Person` class that implements the `Externalizable` interface. This interface requires the implementation of two methods: `writeExternal` for serialization and `readExternal` for deserialization. We manually write and read the object's fields within these methods.

When serializing, the `writeExternal` method is called to write the `name` and `age` fields to the `ObjectOutput` stream. When deserializing, the `readExternal` method is called to read the fields from the `ObjectInput` stream.

Note that `Externalizable` requires a public no-argument constructor, as it needs to create an instance of the object during deserialization. In this example, the `Person` class has a default constructor to fulfill this requirement.

By using externalization, you gain fine-grained control over the serialization and deserialization process. It's often used when you want to customize the serialization of specific fields or manage complex object states during these operations.

## Serialization vs Externalization:

| Aspect          | Serialization                             | Externalization                         |
| --------------- | ----------------------------------------- | --------------------------------------- |
| Mechanism       | Automatic serialization by JVM            | Manual control by developers            |
| Interface       | Implements `Serializable` interface       | Implements `Externalizable` interface   |
| Fields Control  | Serializes all non-transient fields       | Developers explicitly control fields    |
| Customization   | Limited customization options             | High customization flexibility          |
| Performance     | Generally slower due to reflection        | Can be faster due to manual control     |
| Constructor     | No-argument constructor required for read | No-argument constructor required        |
| Default Fields  | Serializes all fields by default          | Developers choose which fields to save  |
| Order of Fields | Fixed order based on class definition     | Manually determine order of fields      |
| Maintenance     | Easier maintenance, less code to write    | More coding effort needed               |
| Backward        | Modifications can cause deserialization   | Provides more control during changes    |
| Compatibility   | May break if fields change significantly  | More resilient to changes in structure  |
| Flexibility     | Less control over serialization process   | More control over serialization process |

In summary, serialization is the default mechanism for object storage in Java, offering automatic serialization of fields and simpler maintenance. Externalization provides developers with more control, customization, and potentially better performance, making it suitable when fine-tuned control over serialization and deserialization is necessary.
