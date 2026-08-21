## What are the key differences between NestJS and Express.js?

- Express.js is a lightweight and flexible Node.js web framework that provides basic tools for building HTTP APIs
- NestJS is a higher-level framework that provides a structured architecture based on modules, controllers, providers and dependency injection.

## Why does NestJS use decorators extensively?

- Decorators such as @Injectable(), @Module(), @Get() allow NestJS to attach metadata to classes, methods and parameters, and users to define the behaviour of each method. 
- For example, @Controller() tells NestJS that file is a controller, @Get() defines an HTTP GET route, and @Injectable() allows a class to be used in dependency injection. This helps make the application explicit and reduce the needs for users to manually express the meaning.

## How does NestJS handle dependency injection?

- NestJS has a built-in dependency injection container. Classes and methods such as services can be registered as providers using @Injectable(), which means those classes and methods could be used in the dependency injection process. 
- When a controller needs to use that service, NestJS can automatically create the service and inject it through the constructor. This breaks the code structure into pieces which makes it easier to be tested.

## What benefits does modular architecture provide in a large-scale app?

- Modular architecture breaks functionalities of an application into small, testable pieces (controllers, services), and then groups related functionalities into modules. 
- This improves maintainability by keeping related code together, reduces coupling between different parts of the application, makes testing easier (since developers know where to find the related functionality), and allows multiple developers to work on different features independently. 
- It also makes large applications easier to scale because new functionality can be added as separate modules without affecting other functionalities (modules).