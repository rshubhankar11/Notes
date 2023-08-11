### `@PathVariable` Annotation

The `@PathVariable` annotation is used to extract values from the URI (path) of a web request. It is typically used when you have dynamic values in the URL, such as IDs or names, that you want to capture and use in your controller method. Here's an example in a Markdown-like format:

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{userId}")
    public ResponseEntity<String> getUserById(@PathVariable Long userId) {
        // Fetch user by ID and perform operations
        return ResponseEntity.ok("User with ID " + userId + " found.");
    }
}
```

In this example, when a request is made to `/users/123`, the value `123` will be extracted from the URL and passed to the `getUserById` method.

### `@RequestParam` Annotation

The `@RequestParam` annotation is used to extract query parameters from the URL. Query parameters are the key-value pairs that appear after the `?` symbol in a URL. This annotation is commonly used when you have optional parameters in your URL. Here's an example:

```java
@RestController
@RequestMapping("/search")
public class SearchController {

    @GetMapping("/byName")
    public ResponseEntity<String> searchByName(@RequestParam String name) {
        // Search for items by name and perform operations
        return ResponseEntity.ok("Search results for name: " + name);
    }
}
```

In this example, a request to `/search/byName?name=apple` would extract the value `apple` from the `name` parameter in the URL and pass it to the `searchByName` method.

Both `@PathVariable` and `@RequestParam` annotations are used to capture data from incoming requests, but they serve different purposes based on where the data is located in the URL. Use `@PathVariable` when the value is in the URL path itself, and use `@RequestParam` when the value is in the query parameters.

## Table :

| Feature           | `@PathVariable` Annotation              | `@RequestParam` Annotation                      |
| ----------------- | --------------------------------------- | ----------------------------------------------- |
| Purpose           | Extract values from the URL path.       | Extract query parameters from the URL.          |
| Usage             | Used for dynamic parts of the URL path. | Used for optional query parameters.             |
| Example URL       | `/users/123`                            | `/search/byName?name=apple`                     |
| Annotation Syntax | `@GetMapping("/{userId}")`              | `@GetMapping("/byName")`                        |
| Method Parameter  | `@PathVariable Long userId`             | `@RequestParam String name`                     |
| Value Extraction  | Extracts value from the URL path.       | Extracts value from the query parameter in URL. |
| Required          | Typically required for path variables.  | Can be optional based on your needs.            |
| URL Flexibility   | Works well for clean and RESTful URLs.  | Suitable for URLs with multiple parameters.     |
| Example Usage     | Fetching a user by their ID.            | Filtering search results based on parameters.   |
