# Implementing Basic Authentication with Spring Security in Spring Boot

#### Step 1: Create a Spring Boot Project

Create a new Spring Boot project using Spring Initializr or your preferred method.

#### Step 2: Add Dependencies

In your `pom.xml` file, add the following dependencies for Spring Security:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

#### Step 3: Configure Security

Create a Java configuration class that extends `WebSecurityConfigurerAdapter` to configure security settings. For example:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/public/**").permitAll()
                .anyRequest().authenticated()
                .and()
            .httpBasic();
    }
}
```

In this example, we permit all requests to `/public/**` and require authentication for all other requests using HTTP Basic Authentication.

#### Step 4: Create User Accounts

You can create user accounts in your Spring Boot application. For simplicity, we'll use an in-memory user store:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;

@Configuration
public class UserDetailsConfig {

    @Bean
    public UserDetailsService userDetailsService() {
        UserDetails user = User.withDefaultPasswordEncoder()
            .username("user")
            .password("password")
            .roles("USER")
            .build();

        return new InMemoryUserDetailsManager(user);
    }
}
```

#### Step 5: Test Basic Authentication

Run your Spring Boot application and access protected endpoints. You will be prompted to enter credentials (username: user, password: password) when accessing secured endpoints.

### Advantages of Basic Authentication

- **Simple to Implement**: Basic Authentication is straightforward to implement and requires minimal configuration.

- **Supported by Most Clients**: It is widely supported by various clients and browsers out-of-the-box, making it a suitable choice for simple authentication needs.

### Disadvantages of Basic Authentication

- **Security Concerns**: Basic Authentication sends credentials in base64-encoded form with each request, which can be easily decoded if intercepted. It lacks strong security features like token-based authentication.

- **Lack of Logout Mechanism**: Basic Authentication does not provide a built-in logout mechanism. To log out, clients often rely on browser-based mechanisms or implement custom solutions.

- **No Token-Based Features**: It doesn't provide features like token expiration, token revocation, or the ability to manage user sessions efficiently.

- **Limited Extensibility**: Basic Authentication may not be suitable for more complex authentication requirements, such as multi-factor authentication.

This basic authentication setup is suitable for simple applications, but for more robust security and features like OAuth2, consider using more advanced authentication methods.

**Note**: Please ensure that you keep sensitive information, such as usernames and passwords, secure. In a production environment, consider using a more secure method for storing user credentials, such as a database or an external authentication provider.

### Save and Retrieve user from Data base

To save and retrieve user credentials from a database in a Spring Boot application with Spring Security using Basic Authentication, you'll need to configure Spring Security to use a custom `UserDetailsService` that interacts with your database. Here's a step-by-step example:

### Step 1: Set up the Database

First, set up a database to store user information. You can use a relational database like MySQL, PostgreSQL, or H2 for this example. Create a table `users` with columns `username`, `password`, and `enabled`.

### Step 2: Create an Entity Class

Create a User entity class that represents a user in your application. This class should be annotated with JPA annotations for persistence.

```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String username;
    private String password;
    private boolean enabled;

    // Constructors, getters, setters, and other necessary methods
}
```

### Step 3: Create a UserRepository

Create a UserRepository interface that extends JpaRepository to interact with the `users` table in the database.

```java
public interface UserRepository extends JpaRepository<User, Long> {
    User findByUsername(String username);
}
```

### Step 4: Implement a Custom UserDetailsService

Create a custom `UserDetailsService` implementation that retrieves user information from the database.

```java
@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username);
        if (user == null) {
            throw new UsernameNotFoundException("User not found with username: " + username);
        }

        // You can customize UserDetails based on your needs (e.g., roles and authorities)
        return new org.springframework.security.core.userdetails.User(
            user.getUsername(),
            user.getPassword(),
            user.isEnabled(),
            true,
            true,
            true,
            getAuthorities("ROLE_USER") // Add user roles/authorities here
        );
    }

    private Collection<? extends GrantedAuthority> getAuthorities(String role) {
        return Collections.singletonList(new SimpleGrantedAuthority(role));
    }
}
```

### Step 5: Configure Spring Security

Configure Spring Security to use your custom `UserDetailsService` and enable Basic Authentication in your `SecurityConfig` class (as shown in the previous example).

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private CustomUserDetailsService userDetailsService;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/public/**").permitAll()
                .anyRequest().authenticated()
                .and()
            .httpBasic();
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService);
    }
}
```

### Step 6: Save User Data to the Database

You can create a controller or use a CommandLineRunner to save user data to the database during application startup. Here's an example using a `CommandLineRunner`:

```java
@Component
public class DatabaseLoader implements CommandLineRunner {

    @Autowired
    private UserRepository userRepository;

    @Override
    public void run(String... args) throws Exception {
        User user = new User();
        user.setUsername("user");
        user.setPassword(new BCryptPasswordEncoder().encode("password"));
        user.setEnabled(true);

        userRepository.save(user);
    }
}
```

In this example, we're using `BCryptPasswordEncoder` to securely encode the user's password before saving it to the database.

Now, your Spring Boot application is configured to save and retrieve user credentials from a database using Spring Security Basic Authentication. Users and their passwords are stored securely in the database, and you can access protected endpoints by providing valid credentials.
