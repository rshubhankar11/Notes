## Let's assume we have a simple Spring Boot application with a service class that performs a division operation and can throw a custom exception if the divisor is zero.

1. Create a custom exception class:

```java
// CustomException.java
public class CustomException extends RuntimeException {
    public CustomException(String message) {
        super(message);
    }
}
```

2. Create a service class that performs the division operation:

```java
// MathService.java
@Service
public class MathService {
    public int divide(int dividend, int divisor) {
        if (divisor == 0) {
            throw new CustomException("Division by zero is not allowed!");
        }
        return dividend / divisor;
    }
}
```

3. Create a controller class to handle the exceptions:

```java
// MathController.java
@RestController
public class MathController {

    @Autowired
    private MathService mathService;

    @GetMapping("/divide")
    public ResponseEntity<Integer> divide(@RequestParam int dividend, @RequestParam int divisor) {
        try {
            int result = mathService.divide(dividend, divisor);
            return ResponseEntity.ok(result);
        } catch (CustomException e) {
            return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(null);
        }
    }

    // Global Exception Handler using @ControllerAdvice
    @ControllerAdvice
    public class GlobalExceptionHandler {

        @ExceptionHandler(CustomException.class)
        public ResponseEntity<String> handleCustomException(CustomException ex) {
            return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(ex.getMessage());
        }

        // For other unhandled exceptions
        @ExceptionHandler(Exception.class)
        public ResponseEntity<String> handleGenericException(Exception ex) {
            return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("An unexpected error occurred.");
        }
    }
}
```

In this example, we have a `MathService` class with a `divide` method that may throw the `CustomException` when the divisor is zero. The `MathController` class has a method `divide` to handle the division operation, and it catches the `CustomException`. We also have a `GlobalExceptionHandler` class defined using `@ControllerAdvice`, which handles the custom exception and also provides a generic exception handler for any other unhandled exceptions.

With this setup, if the division by zero occurs, the `CustomException` will be thrown, and the `GlobalExceptionHandler` will handle it, returning an appropriate response with a 400 Bad Request status and the error message. For any other unhandled exceptions in the application, the generic exception handler will handle them and return a 500 Internal Server Error response.
