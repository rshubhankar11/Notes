# JVM Architecture

## Class Loader Subsystem

The class loader subsystem takes `.class` files as input and performs the following operations:

1. **Load into JVM's Memory:** It loads the `.class` file into the JVM's memory.

2. **Byte Code Verification:** Before loading the `.class` file, it verifies whether the byte code instructions are valid or not with the help of the byte code verifier.

3. **Load Byte Code Instructions:** If the byte code instructions are valid, it loads the byte code instructions into different areas of the JVM known as runtime data areas.

## Runtime Data Areas

These areas are available at runtime to store different types of data. The various runtime data areas are:

1. **Method Area:** This area is used for storing all the class code along with their method code.

2. **Heap:** The heap is used for storing objects.

3. **Java Stack:** This area is used for storing the methods that are under execution. The Java stack can be considered as a collection of frames, where each frame contains the information of only one method.

4. **Program Counter (PC) Register:** This register contains the address of the next instruction that has to be executed.

5. **Java Native Stack:** This area is used for storing non-Java code during the migration of the application from non-Java code to Java code. Non-Java code is referred to as native code.
