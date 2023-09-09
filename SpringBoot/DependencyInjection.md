# Dependency Injection in Spring Boot

Dependency Injection (DI) in Spring Boot is a fundamental concept that allows you to manage and inject dependencies into your Spring Boot applications. It builds upon the Spring Framework's Dependency Injection mechanism and provides a convenient way to develop and manage components, making your application more modular and maintainable.

## Inversion of Control (IoC)

Dependency Injection is a key aspect of IoC, where the control over the creation and management of objects is inverted from your application code to the Spring container. Spring Boot's IoC container, built on top of the Spring Framework, manages the lifecycle of beans and their dependencies.

## Annotations

Spring Boot encourages the use of annotations for configuring and managing beans. Commonly used annotations include:

- `@Autowired`: Used for automatic dependency injection. You can apply it to constructors, fields, or setter methods to indicate the dependencies to be injected.
- `@Component`, `@Service`, `@Repository`: These annotations are used to mark classes as Spring-managed beans. Spring Boot will automatically detect and register these beans.

## Auto Configuration

One of Spring Boot's powerful features is auto-configuration. It automatically configures application components based on the classpath and the dependencies included in your project. For example, if you include a database driver in your project, Spring Boot will configure a data source for you.

## Starter Dependencies

Spring Boot provides starter dependencies, which are pre-configured sets of libraries and configurations for specific tasks, such as web development, data access, and messaging. These starters simplify the setup of common application components and dependencies.

## Externalized Configuration

Spring Boot allows you to externalize configuration settings using properties files (e.g., `application.properties` or `application.yml`). You can define bean properties and various application settings in these files, making it easy to configure your application without code changes.

Here's a simplified example of Dependency Injection in a Spring Boot application:

```java
@Service
public class ProductService {
    private final ProductRepository productRepository;

    @Autowired
    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    // ...
}

@Repository
public class ProductRepository {
    // ...
}
```

In this example, `ProductService` is marked as a Spring-managed service using `@Service`, and it depends on `ProductRepository`, which is marked as a Spring-managed repository using `@Repository`. The `@Autowired` annotation on the constructor of `ProductService` indicates that Spring Boot should automatically inject an instance of `ProductRepository`.

Spring Boot simplifies the configuration and management of dependencies in your application, allowing you to focus on writing business logic. It leverages Spring's Dependency Injection mechanism to wire components together, making your application more modular, testable, and maintainable.
