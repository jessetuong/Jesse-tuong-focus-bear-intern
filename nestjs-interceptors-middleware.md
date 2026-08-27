## What is the difference between an interceptor and middleware in NestJS?

Middleware executes during the request pipeline before the request reaches the controller. It is commonly used for request preprocessing, logging and other HTTP-level operations. Interceptors surround the execution of a controller handler, allowing them to perform actions both before and after the handler executes. They are particularly useful for response transformation, timing, logging, caching and error handling.

## When would you use an interceptor instead of middleware?

An interceptor is preferable when an operation needs access to the controller execution or response. For example, an interceptor can measure how long a controller takes to execute and then log the response time. It can also transform the response after the controller has finished. Middleware is more appropriate when only the incoming request needs to be processed before it reaches the controller.

## How does LoggerErrorInterceptor help?

An error-logging interceptor can centralise error logging for API requests. Instead of adding error logging to every controller, the interceptor can catch errors as they pass through the request pipeline, log useful diagnostic information and then rethrow the error so NestJS can handle the response. LoggerErrorInterceptor is not a standard NestJS built-in interceptor, so its exact behaviour depends on the implementation used by the project.