1. What are the benefits of using nestjs-pino for logging?

- nestjs-pino integrates the high-performance Pino logging library with NestJS. It provides structured JSON logging, request and response information, log levels, and useful metadata for debugging. Structured logs are easier for monitoring systems to search, filter, and analyse than plain text logs. Pino is also designed to have low performance overhead, making it suitable for production applications.

2. How does global exception handling improve API consistency?

- A global exception filter ensures that errors from different parts of the application are returned using a consistent format. Instead of each controller creating its own error response, the filter can provide common fields such as the HTTP status code, error message, timestamp, and request path. This makes it easier for frontend and mobile applications to handle errors consistently.

3. What is the difference between a logging interceptor and an exception filter?

- A logging interceptor operates around the request/response lifecycle and can record information such as the HTTP method, URL, response status, and processing time. An exception filter specifically handles exceptions and determines how errors should be processed and returned to the client. An interceptor can observe errors, but an exception filter is specifically designed to handle and format them.

4. How can logs be structured to provide useful debugging information?

- Useful structured logs should contain relevant information such as timestamps, log levels, HTTP methods, request URLs, status codes, response times, error messages, and request or correlation identifiers where appropriate. Structured JSON allows monitoring tools to search and analyse these fields efficiently. Sensitive information such as passwords, access tokens, and API keys should never be included in logs.