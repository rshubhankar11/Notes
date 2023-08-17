# JUnit Testing in Java Spring Boot

JUnit is a widely-used testing framework for Java that is primarily used for unit testing. It allows developers to write test cases to verify the correctness of their code. In the context of Java Spring Boot applications, JUnit is often used to test individual components, services, and controllers.

## Mockito

Mockito is a mocking framework for Java that allows you to create mock objects in your tests. Mock objects simulate the behavior of real objects, making it easier to isolate and test specific parts of your application.

## PowerMock

PowerMock is an extension to Mockito and other mocking frameworks. It enables you to mock static methods, final classes, and other constructs that are typically challenging to mock using standard mocking frameworks.

### Mockito vs. PowerMock: Differences

| Feature                  | Mockito                                                           | PowerMock                                                                                 |
| ------------------------ | ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Mocking                  | Supports mocking of non-final classes, interfaces, and objects.   | Extends Mockito and allows mocking of static methods, final classes, constructors, etc.   |
| Limitations              | Cannot mock static methods, final classes, and constructors.      | Overcomes the limitations of Mockito by providing more advanced mocking capabilities.     |
| Use Cases                | Suitable for most scenarios where advanced mocking is not needed. | Used when advanced mocking of static methods, final classes, or constructors is required. |
| Integration with Mockito | Can be used alongside Mockito for basic mocking needs.            | Requires both Mockito and PowerMock libraries.                                            |
| Learning Curve           | Relatively easy to learn and use.                                 | More complex due to additional capabilities.                                              |

### Example: JUnit Testing with Mockito and PowerMock

Assume you have a `CalculatorService` class with a method `add` that you want to test. You also have a `MathUtils` class with a static method `divide` that you want to mock.

```java
// CalculatorService.java
public class CalculatorService {
    public int add(int a, int b) {
        return a + b;
    }
}

// MathUtils.java
public class MathUtils {
    public static int divide(int dividend, int divisor) {
        if (divisor == 0) {
            throw new ArithmeticException("Cannot divide by zero");
        }
        return dividend / divisor;
    }
}
```

#### Test Case Using JUnit, Mockito, and PowerMock

```java
import static org.mockito.Mockito.*;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.powermock.api.mockito.PowerMockito;
import org.powermock.core.classloader.annotations.PrepareForTest;
import org.powermock.modules.junit4.PowerMockRunner;

@RunWith(PowerMockRunner.class)
@PrepareForTest({MathUtils.class})
public class CalculatorServiceTest {

    @InjectMocks
    private CalculatorService calculatorService;

    @Mock
    private MathUtils mathUtilsMock;

    @Test
    public void testAddWithMocking() {
        PowerMockito.mockStatic(MathUtils.class);
        when(MathUtils.divide(anyInt(), anyInt())).thenReturn(2);

        int result = calculatorService.add(3, 5);

        assertEquals(8, result);
        verify(mathUtilsMock, never()).someMethodToMock();
    }

    @Test(expected = ArithmeticException.class)
    public void testDivideByZero() {
        PowerMockito.mockStatic(MathUtils.class);
        when(MathUtils.divide(anyInt(), eq(0))).thenThrow(new ArithmeticException("Cannot divide by zero"));

        calculatorService.add(10, 0);
    }
}
```

### Handling Exceptions in JUnit

You can use the `@Test(expected = YourExpectedException.class)` annotation to specify that a test method is expected to throw a certain exception.

```java
@Test(expected = ArithmeticException.class)
public void testDivideByZero() {
    int result = mathUtils.divide(10, 0);
}
```

To handle exceptions more flexibly, you can use try-catch blocks within your test methods.

```java
@Test
public void testDivideByZeroHandled() {
    try {
        int result = mathUtils.divide(10, 0);
        fail("Expected ArithmeticException, but no exception was thrown.");
    } catch (ArithmeticException e) {
        assertEquals("Cannot divide by zero", e.getMessage());
    }
}
```

---

Feel free to adjust the example code to match your actual classes and scenarios. Also, ensure that you have the required dependencies added to your Maven `pom.xml` file. This guide provides a basic overview, and you may need to refer to official documentation and resources for more detailed usage.

## Testing Controller with JUnit testing :

Testing controllers in JUnit involves creating mock objects for your service or business logic and then using those mock objects to simulate requests to your controller. You can also utilize frameworks like Mockito to assist in creating these mock objects and to verify the behavior of your controller methods. Here's a step-by-step guide on how to test a controller using JUnit:

1. **Set Up Dependencies and Annotations:**

   In your JUnit test class, you need to set up the necessary annotations to indicate that you're using JUnit and to enable mockito support. Also, you should use `@WebMvcTest` annotation to indicate that you want to perform a controller test. This annotation will auto-configure a Spring MVC context and initialize only the beans related to MVC, not the whole application context.

```java
@RunWith(SpringRunner.class)
@WebMvcTest(YourController.class)
public class YourControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private YourService yourService; // Mock your service here

    // Your test methods go here
}
```

2. **Write Test Methods:**

   Now, you can write test methods to cover different scenarios for your controller methods. Use `MockMvc` to perform requests and verify responses.

```java
@Test
public void testGetAllItems() throws Exception {
    List<Item> mockItemList = new ArrayList<>();
    mockItemList.add(new Item(1, "Item 1"));

    when(yourService.getAllItems()).thenReturn(mockItemList);

    mockMvc.perform(get("/items"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$", hasSize(1)))
            .andExpect(jsonPath("$[0].id", is(1)))
            .andExpect(jsonPath("$[0].name", is("Item 1")));

    verify(yourService, times(1)).getAllItems();
}
```

In this example, we are testing a controller method that fetches a list of items. We've mocked the `YourService` dependency using `@MockBean` and defined the behavior using `when(...).thenReturn(...)`.

3. **Verify Controller Behavior:**

   Use `andExpect` to verify the behavior of your controller, like checking response status, response content, and so on.

4. **Verify Service Interactions:**

   Use Mockito's `verify` methods to ensure that the expected interactions with the service methods are happening.

5. **Handle Exception Scenarios:**

   To test exception scenarios, you can use the `.andExpect(MockMvcResultMatchers::exception)` along with the specific exception class you expect to be thrown.

```java
@Test
public void testGetItemByIdNotFound() throws Exception {
    int itemId = 123;

    when(yourService.getItemById(itemId)).thenThrow(new ItemNotFoundException("Item not found"));

    mockMvc.perform(get("/items/{id}", itemId))
            .andExpect(status().isNotFound())
            .andExpect(jsonPath("$.message", is("Item not found")));

    verify(yourService, times(1)).getItemById(itemId);
}
```

Remember to customize these examples to match your actual controller methods, service methods, and business logic.

6. **Add Necessary Dependencies:**

   Ensure that you have the necessary dependencies in your `pom.xml` for Spring Boot, Spring Test, and Mockito.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>...</version>
    <scope>test</scope>
</dependency>
```

By following these steps, you can effectively test your Spring MVC controllers using JUnit and Mockito. Remember to mock the service or business logic layer and then verify the behavior of the controller methods and their interactions.
