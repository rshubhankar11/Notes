# Microservice Notes

## Config Server:

1. Config Server use to handel common configuration of diffrent microservices so
   that we dont have to repeat same configuration in every service .
   b. For example we have comon configuration of our Eureka client in every service
   for that we can create a cofig server and in other services we can simply
   refer to our config server.
2. To setup config server we have to use dependacy:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

3. We have to create a git repo where we will store our application.yml file
   for diffrent diffrent sping profile for example application-dev.yml and
   application-prod.yml
4. config-server properties configuration:

```YML
spring:
  application:
    name: CONFI-SERVER

  cloud:
    config:
      server:
        git:
          uri: https://github.com/rshubhankar11/Microservice-Configurations
          clone-on-start: true
```

5. config-server properties to use in client service:

```YML
spring:
  config:
    import: optional:configserver:http://localhost:8085
```

## Service-Registry:

1. Useing service-Registry we can register all our services.
2. For example if you want to access one service in another servies then
   we have to use port number and the the api path. But that port number
   can be changed at any time . So if it got changed the application will break.
3. If you have registered our service in service-registry then we can call the
   service with its name instead of port number . And in feature if the port
   number changed that will not impact our services.
4. Deppendacy :

```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter</artifactId>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-netflix-eureka-server -->
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

4. We have to annotate our main application class with :

```java
@EnableEurekaServer
```

5. properties configuration:

```properties
server.port=8761
eureka.instance.hostname=localhost
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

6. In order to register one service under our service registry we have to add
   Eureka client dependancy:

```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

> And use @EnableEurekaClient on the main class.

7. properties configuration for registration :

```yml
#Eureka client setup
eureka:
  instance:
    prefer-ip-address: true
  client:
    fetch-registry: true
    register-with-eureka: true
    service-url:
    	defaultZone: http://localhost:8761/eureka
```

## API-Getway:

1. API-Getway as the name suggested it act like a get way to our microservices.
2. We can call all our services using API-Getway.
3. Request form front end/user will come to API-Getway and then it decides
   whic service it should call.
4. We can implement spring scurity to our API-Getway in ourder to scure our services .
5. Dependacy:

```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

6. Configuraion:

```yml
    	spring:
    	  application:
    	    name: API-GATEWAY

    	  #API GATEWAY Setup
    	  cloud:
    	    gateway:
    	      routes:
    	        - id: USER-SERVICE
    	          uri: lb://USER-SERVICE
    	          predicates:
    	            - Path=/users/**

    	        - id: HOTEL-SERVICE
    	          uri: lb://HOTEL-SERVICE
    	          predicates:
    	            - Path=/hotels/**

    	        - id: RATING-SERVICE
    	          uri: lb://RATING-SERVICE
    	          predicates:
    	            - Path=/ratings/**

```
