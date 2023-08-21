# HTTP Status Codes in Spring Boot RestTemplate

HTTP status codes indicate the outcome of a HTTP request made through a RestTemplate in Spring Boot applications.

## Informational Responses (1xx)

- **100 Continue:** The server has received the request headers and the client should proceed to send the request body.
- **101 Switching Protocols:** The server indicates that it is changing protocols and the client should switch to the new protocol.

## Successful Responses (2xx)

- **200 OK:** The request has succeeded.
- **201 Created:** The request has been fulfilled, resulting in the creation of a new resource.
- **202 Accepted:** The request has been accepted for processing, but processing has not been completed.
- **204 No Content:** The server successfully processed the request but there's no response body to send.

## Redirection Responses (3xx)

- **300 Multiple Choices:** The requested resource has multiple choices and the user or agent can select one.
- **301 Moved Permanently:** The requested resource has moved permanently to a new location.
- **302 Found:** The requested resource has moved temporarily to a different location.
- **303 See Other:** The response to the request can be found under a different URI.
- **304 Not Modified:** The requested resource has not been modified since the last request.

## Client Error Responses (4xx)

- **400 Bad Request:** The server cannot understand the request.
- **401 Unauthorized:** The client must authenticate itself to get the requested response.
- **403 Forbidden:** The client does not have the necessary permissions.
- **404 Not Found:** The server cannot find the requested resource.
- **405 Method Not Allowed:** The method specified in the request is not allowed for the resource.

## Server Error Responses (5xx)

- **500 Internal Server Error:** A generic error message indicating that the server encountered an error.
- **501 Not Implemented:** The server does not have the functionality to fulfill the request.
- **502 Bad Gateway:** The server, while acting as a gateway or proxy, received an invalid response from an upstream server.
- **503 Service Unavailable:** The server is not ready to handle the request.
- **504 Gateway Timeout:** The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server.

For more detailed information, refer to the [HTTP status code definitions](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

Please note that this is not an exhaustive list of HTTP status codes, but covers the most commonly used ones in the context of Spring Boot's RestTemplate.
