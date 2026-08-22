## What files are included in a default NestJS project?

- A project has files such as main.ts, app.module.ts, app.controller.ts, app.service.ts, configuration files such as nest-cli.json and TypeScript configuration files, as well as testing files. 
- main.ts acts as the entry point, while the Module, Controller and Service form the basic NestJS architecture.

## How does main.ts bootstrap a NestJS application?

- main.ts uses NestFactory.create() to create a NestJS application using AppModule as the root module. It then calls app.listen() to start the HTTP server, normally on port 3000. This makes main.ts the starting point from which NestJS loads the application’s modules, controllers and providers.

## What is the role of AppModule?

- AppModule is the root module of a NestJS application. It acts as the main container for the application’s modules, controllers and providers. As the application grows, additional feature modules can be imported into AppModule, allowing the application to remain organised.

## How does NestJS structure help with scalability?

- NestJS uses modules, controllers and services to separate different responsibilities within an application. Related functionality can be grouped into feature modules, while controllers handle HTTP requests and services contain business logic. This separation makes large applications easier to maintain, test and extend, and allows different developers or teams to work on separate parts of the system.