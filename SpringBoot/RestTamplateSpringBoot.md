## Here's a complete example of using `RestTemplate` in a Spring Boot application to call an external API. In this example, we'll use the `RestTemplate` to fetch data from the GitHub API.

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
