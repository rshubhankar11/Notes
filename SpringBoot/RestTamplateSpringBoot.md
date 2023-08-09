# RestTameplate :

### Here's a complete example of using `RestTemplate` in a Spring Boot application to call an external API. In this example, we'll use the `RestTemplate` to fetch data from the GitHub API.

1. Create a simple model class to hold the response from the API:

```java
// GitHubRepo.java
public class GitHubRepo {
    private String name;
    private String html_url;

    // Getters and setters
}
```

2. Create a service class that uses `RestTemplate` to fetch data from the API:

```java
// GitHubService.java
@Service
public class GitHubService {

    private final RestTemplate restTemplate;

    public GitHubService(RestTemplateBuilder restTemplateBuilder) {
        this.restTemplate = restTemplateBuilder.build();
    }

    public GitHubRepo getRepositoryInfo(String owner, String repoName) {
        String apiUrl = "https://api.github.com/repos/" + owner + "/" + repoName;
        ResponseEntity<GitHubRepo> responseEntity = restTemplate.exchange(apiUrl, HttpMethod.GET, null, GitHubRepo.class);
        if (responseEntity.getStatusCode() == HttpStatus.OK) {
            return responseEntity.getBody();
        } else {
            throw new RuntimeException("Failed to fetch repository info.");
        }
    }
}
```

3. Create a controller class to expose an API endpoint that uses the service to fetch data:

```java
// GitHubController.java
@RestController
public class GitHubController {

    private final GitHubService gitHubService;

    public GitHubController(GitHubService gitHubService) {
        this.gitHubService = gitHubService;
    }

    @GetMapping("/repos/{owner}/{repoName}")
    public ResponseEntity<GitHubRepo> getRepositoryInfo(@PathVariable String owner, @PathVariable String repoName) {
        GitHubRepo repo = gitHubService.getRepositoryInfo(owner, repoName);
        return ResponseEntity.ok(repo);
    }
}
```

4. Configure `RestTemplate` in your Spring Boot configuration class:

```java
// ApplicationConfig.java
@Configuration
public class ApplicationConfig {

    @Bean
    public RestTemplate restTemplate(RestTemplateBuilder builder) {
        return builder.build();
    }
}
```

5. Finally, create the main Spring Boot application class:

```java
// MySpringBootApplication.java
@SpringBootApplication
public class MySpringBootApplication {

    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

Now, when you run the Spring Boot application and make a GET request to `/repos/{owner}/{repoName}`, it will call the GitHub API to fetch the repository information for the specified owner and repository name using `RestTemplate`. The `GitHubService` class handles the API call, and the fetched data is returned to the client as JSON through the `GitHubController`.

Make sure you have `spring-boot-starter-web` and `spring-boot-starter-web-services` dependencies in your `pom.xml` or `build.gradle` to have access to the required libraries for web development and `RestTemplate`.

--

## PUT vs POST vs PATCH

`PUT`, `POST`, and `PATCH` are HTTP methods used in web development to perform different actions on resources (typically represented by URLs) within a web application. Each method has a distinct purpose and use case:

1. **POST (Create):**

   - The `POST` method is used to submit data to the server to create a new resource.
   - It's often used when you want to create a new entry or record on the server.
   - The server usually generates a new URI for the resource and returns it in the response.
   - `POST` requests are not idempotent, meaning multiple identical requests may have different effects.

2. **PUT (Update):**

   - The `PUT` method is used to update or create a resource at a specific URL.
   - It's typically used to update an existing resource, and if the resource doesn't exist, it might create a new resource with the given URL.
   - When using `PUT`, you need to send the entire updated resource representation to the server.
   - `PUT` requests are idempotent, meaning making the same request multiple times should have the same result as making it once.

3. **PATCH (Partial Update):**
   - The `PATCH` method is used to apply partial modifications to a resource.
   - Unlike `PUT`, you only send the changes you want to apply to the server, rather than the entire updated representation.
   - This can be useful when you want to update only specific fields of a resource without affecting the others.
   - Like `PUT`, `PATCH` requests are also idempotent.

In summary:

- **POST** is used to create a new resource on the server.
- **PUT** is used to update or create a resource at a specific URL.
- **PATCH** is used to apply partial updates to a resource.

It's important to use these methods correctly according to their intended purposes to ensure the proper functioning and design of your web application's API.

Certainly, here's a comparison of the `PUT`, `POST`, and `PATCH` HTTP methods in a tabular format:

| Method | Purpose                     | Idempotent | Payload        | Resource Creation | Partial Updates |
| ------ | --------------------------- | ---------- | -------------- | ----------------- | --------------- |
| POST   | Create a new resource       | No         | Data included  | Yes               | No              |
| PUT    | Update or create a resource | Yes        | Entire update  | Yes (if absent)   | No              |
| PATCH  | Partially update a resource | Yes        | Partial update | No                | Yes             |

Please note that the information in this table is based on the typical use cases and characteristics of these HTTP methods. However, the actual behavior might vary depending on the specific implementation and API design.
