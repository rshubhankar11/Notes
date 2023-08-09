# @Value

In Spring Boot, the `@Value` annotation is used to inject values from external sources, such as properties files, environment variables, or command-line arguments, into Spring beans. It allows you to externalize configuration and make your application more flexible by allowing you to change values without modifying your code.

Here's a simple explanation with an example:

Let's say you have a Spring Boot application that needs to read a configuration value from an external source. You can use the `@Value` annotation to inject this value into a Spring bean.

1. **Define a property in your `application.properties` file:**

Assuming you have an `application.properties` file in your Spring Boot project, you can define a property like this:

```properties
app.max-users=100
```

2. **Inject the property using `@Value` in a Spring Bean:**

Suppose you have a Spring bean that needs to use the `max-users` value. You can inject it using the `@Value` annotation like this:

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class UserService {

    @Value("${app.max-users}")  // Injects the value of 'app.max-users' property
    private int maxUsers;

    public void printMaxUsers() {
        System.out.println("Max Users: " + maxUsers);
    }
}
```

In this example, the `@Value("${app.max-users}")` annotation injects the value of the `app.max-users` property into the `maxUsers` field of the `UserService` bean.

3. **Using the injected property:**

You can now use the injected property within your bean's methods:

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class MyApp {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(MyApp.class, args);

        UserService userService = context.getBean(UserService.class);
        userService.printMaxUsers();

        context.close();
    }
}
```

When you run your Spring Boot application, it will read the value of `app.max-users` from the properties file and inject it into the `maxUsers` field of the `UserService` bean. The `printMaxUsers` method then prints this value.

The `@Value` annotation is quite handy for injecting simple configuration values into your beans. However, for more advanced scenarios and complex configuration, Spring provides other mechanisms like `@ConfigurationProperties` or `Environment` to manage properties and configurations.
