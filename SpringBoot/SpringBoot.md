# Spring Boot

## What is Spring Boot ?

- Spring Boot is a Spring module which provides RAD (Rapid Application Development) feature to Spring framework.

- It is used to create stand alone spring based application that you can just run because it needs very little spring configuration.

- [Complete Guide](https://www.javatpoint.com/spring-boot-tutorial)

## What are the advantages of Spring Boot ?

- Create stand-alone Spring applications that can be started using java -jar.
- Embed Tomcat, Jetty or Undertow directly. You don't need to deploy WAR files.
- It provides opinionated 'starter' POMs to simplify your Maven configuration.
- It automatically configure Spring whenever possible.

## Advantages of Spring Boot :

- It creates stand-alone Spring applications that can be started using Java -jar.
- It tests web applications easily with the help of different Embedded HTTP servers such as Tomcat, Jetty, etc. We don't need to deploy WAR files.
- It provides opinionated 'starter' POMs to simplify our Maven configuration.
- It provides production-ready features such as metrics, health checks, and externalized configuration.
- There is no requirement for XML configuration.
- It offers a CLI tool for developing and testing the Spring Boot application.
- It offers the number of plug-ins.
- It also minimizes writing multiple boilerplate codes (the code that has to be included in many places with little or no alteration), XML configuration, and annotations.
- It increases productivity and reduces development time.

## Limitations of Spring Boot :

- Spring Boot can use dependencies that are not going to be used in the application. These dependencies increase the size of the application.

## Goals of Spring Boot :

> The main goal of Spring Boot is to reduce development, unit test, and integration test time.

- Provides Opinionated Development approach
- Avoids defining more Annotation Configuration
- Avoids writing lots of import statements
- Avoids XML Configuration.

By providing or avoiding the above points, Spring Boot Framework reduces Development time, Developer Effort, and increases productivity.

## Spring Boot Features :

- **Web Development** :
  - It is a well-suited Spring module for web application development. We can easily create a self-contained HTTP application that uses embedded servers like **Tomcat, Jetty,** or Undertow. We can use the **spring-boot-starter-web**module to start and run the application quickly.
- **SpringApplication** :

  - The SpringApplication is a class that provides a convenient way to bootstrap a Spring application. It can be started from the main method. We can call the application just by calling a static run() method.

  ```Java

  public static void main(String[] args)
  {
      SpringApplication.run(ClassName.class, args);
  }

  ```

- **Application events and listeners** :
  - Spring Boot uses events to handle the variety of tasks. It allows us to create factories file that is used to add listeners. We can refer it to using the **ApplicationListener key**.
  - Always create factories file in META-INF folder like META-INF/spring.factories.
- **Admin features**:
  - Spring Boot provides the facility to enable admin-related features for the application. It is used to access and manage applications remotely. We can enable it in the Spring Boot application by using **spring.application.admin.enabled** property.
- **Externalized Configuration** :
  - Spring Boot allows us to externalize our configuration so that we can work with the same application in different environments. The application uses YAML files to externalize configuration.
- **Properties Files** :
  - Spring Boot provides a rich set of **Application Properties**. So, we can use that in the properties file of our project. The properties file is used to set properties like **server-port =8082** and many others. It helps to organize application properties.
- **YAML Support** :
  - It provides a convenient way of specifying the hierarchical configuration. It is a superset of JSON. The SpringApplication class automatically supports YAML. It is an alternative of properties file.
- **Type-safe Configuration** :
  - The strong type-safe configuration is provided to govern and validate the configuration of the application. Application configuration is always a crucial task which should be type-safe. We can also use annotation provided by this library.
- **Logging** :
  - Spring Boot uses Common logging for all internal logging. Logging dependencies are managed by default. We should not change logging dependencies if no customization is needed.
- **Security** :
  - Spring Boot applications are spring bases web applications. So, it is secure by default with basic authentication on all HTTP endpoints. A rich set of Endpoints is available to develop a secure Spring Boot application.

## What are the Spring Boot Annotations ?

- The @RestController is a stereotype annotation. It adds @Controller and @ResponseBody annotations to the class. We need to import org.springframework.web.bind.annotation package in our file, in order to implement it.

## What is Spring Boot dependency management ?

- Spring Boot manages dependencies and configuration automatically. You don't need to specify version for any of that dependencies.
- Spring Boot dependency management is a feature of Spring Boot that allows you to manage the dependencies of your Spring Boot application in a centralized location. This makes it easy to keep track of the dependencies that your application uses, and to ensure that they are all compatible with each other.
- Here are some of the benefits of using Spring Boot dependency management:

  - **Centralized dependency management**: All of the dependencies of your Spring Boot application are managed in a single location. This makes it easy to keep track of the dependencies that your application uses, and to ensure that they are all compatible with each other.
  - **Automatic dependency resolution**: Maven will automatically resolve all of the dependencies that are defined in the BOM. This means that you don't have to worry about manually specifying the versions of the dependencies that you use.
  - **Compatibility assurance**: Spring Boot dependency management helps to ensure that your application is compatible with all of the dependencies that it uses. This is because the BOMs that Spring Boot provides are carefully curated to ensure that they are compatible with each other.

## What are the Spring Boot Starters ?

- Starters are a set of convenient dependency descriptors which we can include in our application.
- Spring Boot provides built-in starters which makes development easier and rapid. For example, if we want to get started using Spring and JPA for database access, just include the **spring-boot-starter-data-jpa** dependency in your project.

## What is @RestController annotation in Spring Boot ?

- The @RestController is a stereotype annotation. It adds @Controller and @ResponseBody annotations to the class. We need to import org.springframework.web.bind.annotation package in our file, in order to implement it.

## Spring Boot Actuator :

- Spring Boot Actuator is a sub-project of the Spring Boot Framework. It includes a number of additional features that help us to monitor and manage the Spring Boot application. It contains the actuator endpoints (the place where the resources live). We can use HTTP and JMX endpoints to manage and monitor the Spring Boot application. If we want to get production-ready features in an application, we should use the Spring Boot actuator.

- [Detailed description](https://www.javatpoint.com/spring-boot-actuator)

## Spring Vs Spring Boot ?

- Spring is a web application framework based on Java. It provides tools and libraries to create a complete cutomized web application.
- Wheras Spring Boot is a spring module which is used to create spring application project that can just run.
