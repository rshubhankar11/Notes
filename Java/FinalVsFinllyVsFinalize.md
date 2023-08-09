# Final vs Finally vs Finalize :

1. **final:**

   - `final` is a keyword in Java that can be applied to variables, methods, and classes.
   - When applied to a variable, it indicates that the variable's value cannot be changed once it's assigned.
   - When applied to a method, it indicates that the method cannot be overridden by subclasses.
   - When applied to a class, it indicates that the class cannot be extended (subclassed).
   - Example:

     ```java
     final int constantValue = 10;

     final class FinalClass {
         // Class definition
     }

     public final void doSomething() {
         // Method definition
     }
     ```

2. **finally:**

   - `finally` is a block in Java used in conjunction with `try`-`catch` blocks to ensure that a certain block of code gets executed regardless of whether an exception is thrown or not.
   - The `finally` block is used for cleanup tasks and releasing resources that need to be performed regardless of whether an exception occurs.
   - Example:
     ```java
     try {
         // Code that might throw an exception
     } catch (Exception e) {
         // Handle the exception
     } finally {
         // Code that will always be executed
     }
     ```

3. **finalize:**

   - `finalize` is a method defined in the `Object` class in Java.
   - It's called by the garbage collector when it determines that there are no more references to the object.
   - The `finalize` method allows an object to perform cleanup operations before it is reclaimed by the garbage collector.
   - However, it's generally not recommended to rely on `finalize` for cleanup, as its invocation is not guaranteed and might have performance implications.
   - Example:

     ```java
     class MyObject {
         // Other members and methods

         @Override
         protected void finalize() throws Throwable {
             // Cleanup operations before the object is garbage collected
             super.finalize();
         }
     }
     ```

In summary:

- `final` is used to indicate immutability (for variables), prevent method overriding (for methods), or prevent subclassing (for classes).
- `finally` is used in exception handling to ensure a block of code gets executed regardless of exceptions.
- `finalize` is a method used for cleanup operations before an object is garbage collected, though it's not commonly used due to its limitations.

Make sure to use these terms in the appropriate context to avoid confusion in your Java programming.

## Comparison Table

Certainly! Here's a comparison table between "final," "finally," and "finalize" in Java:

| Term       | Purpose and Usage                                                                                                                                    | Example(s)                                                                                                       |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `final`    | Keyword used for variables, methods, and classes to indicate immutability, prevent method overriding, or prevent subclassing.                        | `final int constantValue = 10;`<br>`final class FinalClass { ... }`<br>`public final void doSomething() { ... }` |
| `finally`  | Block used with `try`-`catch` blocks to ensure specified code runs regardless of exceptions.                                                         | `java try { ... } catch (Exception e) { ... } finally { ... } `                                                  |
| `finalize` | Method defined in the `Object` class for cleanup operations before an object is garbage collected, though it's not commonly used due to limitations. | `java @Override protected void finalize() throws Throwable { ... } `                                             |

Keep in mind that each of these terms serves a distinct purpose in Java programming and should be used in the appropriate context.
