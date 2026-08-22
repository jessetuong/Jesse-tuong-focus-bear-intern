## What is the purpose of a module in NestJS?

- A module groups related functionality together, such as controllers and providers. It contains functionality of a specific feature (auth, booking,...) so an application are broken into meaningful sections.

## How does a controller differ from a provider?

- A controller is responsible for handling incoming HTTP requests and returning responses, while a provider contains business logic that can be injected into other components and used. Services are usually providers in NestJS

## Why is dependency injection useful in NestJS?

- Dependency injection allows NestJS to create and provide business logics and dependencies to components that need it. This reduces tight coupling between components, makes code easier to test and allows implementations to be replaced without changing the classes that depend on them.

## How does NestJS ensure modularity and separation of concerns?

- NestJS uses modules to group related controllers and providers. Each one handles separate tasks (for example, controllers focus on handling HTTP requests, while providers handle business logic). This separation makes large applications easier to maintain and extend.