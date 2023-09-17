# Spring Bean Scopes in Spring Boot

In Spring Boot, as well as in the broader Spring Framework, a "bean scope" refers to the lifecycle and visibility of a bean instance within the Spring application context. Spring offers several bean scopes to control how beans are created, shared, and destroyed. Each scope defines the boundaries within which a bean can be accessed, and different scopes are suitable for different use cases. Here are some commonly used bean scopes in Spring Boot:

1. **Singleton (default)**:

   - **Scope Name**: `singleton`
   - **Description**: By default, all Spring beans are singleton scoped, meaning there's only one instance of the bean per Spring container (application context). This single instance is shared across all requests or injections, making it suitable for stateless beans, such as service classes.

   ```java
   @Service // Singleton scope is the default
   public class MyService {
       // ...
   }
   ```

2. **Prototype**:

   - **Scope Name**: `prototype`
   - **Description**: In prototype scope, a new instance of the bean is created every time it's requested from the container. This allows for a fresh instance with each injection, suitable for stateful or non-thread-safe beans.

   ```java
   @Scope("prototype")
   @Component
   public class MyPrototypeBean {
       // ...
   }
   ```

3. **Request**:

   - **Scope Name**: `request`
   - **Description**: A new instance of the bean is created for each HTTP request. This scope is primarily used in web applications to ensure that each user request receives its own isolated instance of a bean.

   ```java
   @Scope(value = WebApplicationContext.SCOPE_REQUEST, proxyMode = ScopedProxyMode.TARGET_CLASS)
   @Component
   public class MyRequestScopedBean {
       // ...
   }
   ```

4. **Session**:

   - **Scope Name**: `session`
   - **Description**: A new instance of the bean is created for each user session in a web application. It ensures that each user's session data is isolated from others.

   ```java
   @Scope(value = WebApplicationContext.SCOPE_SESSION, proxyMode = ScopedProxyMode.TARGET_CLASS)
   @Component
   public class MySessionScopedBean {
       // ...
   }
   ```

5. **Application (ServletContext)**:

   - **Scope Name**: `application`
   - **Description**: A single instance of the bean is created for the entire web application. It's shared across all users and sessions within the application.

   ```java
   @Scope(value = WebApplicationContext.SCOPE_APPLICATION, proxyMode = ScopedProxyMode.TARGET_CLASS)
   @Component
   public class MyApplicationScopedBean {
       // ...
   }
   ```

6. **WebSocket**:

   - **Scope Name**: `websocket`
   - **Description**: A new instance of the bean is created for each WebSocket connection. This scope is used in WebSocket-based applications to provide a separate instance for each connected WebSocket session.

   ```java
   @Scope(value = "websocket", proxyMode = ScopedProxyMode.TARGET_CLASS)
   @Component
   public class MyWebSocketScopedBean {
       // ...
   }
   ```

These are some of the common bean scopes available in Spring Boot. Choosing the appropriate scope for your beans is important to ensure the correct behavior and performance of your application. The default scope for Spring Boot components like `@Service`, `@Repository`, and `@Controller` is usually singleton, but you can customize the scope as needed for specific use cases.
