## How does a Dockerfile define a containerized NestJS application?

A Dockerfile defines the environment and instructions required to build and run the NestJS application. It specifies the base Node.js image, installs dependencies, copies the source code, builds the TypeScript application, exposes the application port and defines the command used to start NestJS.

## What is the purpose of a multi-stage build?

A multi-stage build separates the build environment from the production environment. The first stage compiles the NestJS application, while the final stage contains only the compiled application and production dependencies. This can reduce image size and avoid unnecessary development tools in the runtime image.

## How does Docker Compose simplify running multiple services together?

Docker Compose allows multiple services, such as NestJS and PostgreSQL, to be defined in one configuration file. It creates the necessary network between them, manages their containers, environment variables, ports, volumes and dependencies, allowing the entire development environment to be started with a single command.

## How can you expose API logs and debug a running container?

Docker Compose provides commands such as docker compose logs and docker compose logs -f for viewing application logs. A running container can also be inspected or debugged using commands such as docker exec -it <container> sh, while docker compose ps can be used to check the status of the services.