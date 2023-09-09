# Using Jetty Server in Spring Boot

To replace the default Tomcat server with the Jetty server in a Spring Boot application, follow these steps:

1. **Update `pom.xml`**:

   In your `pom.xml` file, exclude the Tomcat starter and include the Jetty starter. Here's an example:

   ```xml
   <!-- Remove Tomcat starter -->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-web</artifactId>
       <exclusions>
           <exclusion>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-tomcat</artifactId>
           </exclusion>
       </exclusions>
   </dependency>

   <!-- Add Jetty starter -->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-jetty</artifactId>
   </dependency>
   ```

2. **Configure Port (Optional)**:

   By default, Spring Boot uses port 8080 for the embedded server. You can configure a different port if needed. Add this to your `application.properties` or `application.yml`:

   ```properties
   server.port=8081
   ```

   This will change the server's port to 8081.

3. **Run Your Application**:

   Now, you can run your Spring Boot application as usual. Spring Boot will use the Jetty server instead of Tomcat.

That's it! You have replaced the Tomcat server with the Jetty server in your Spring Boot application.

Remember to refresh your Maven project to apply the changes to your dependencies.

Here's an example of a `pom.xml` file with the necessary changes:

```xml
<!-- pom.xml -->

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>my-spring-boot-app</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.6.0</version> <!-- Use the appropriate Spring Boot version -->
    </parent>

    <dependencies>
        <!-- Remove Tomcat starter -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <exclusions>
                <exclusion>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-tomcat</artifactId>
                </exclusion>
            </exclusions>
        </dependency>

        <!-- Add Jetty starter -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jetty</artifactId>
        </dependency>
    </dependencies>

    <properties>
        <!-- Specify Java version -->
        <java.version>11</java.version>
    </properties>
</project>
```

With these changes, your Spring Boot application will use the Jetty server instead of Tomcat for serving your web application.
