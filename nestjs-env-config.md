1. How does @nestjs/config help manage environment variables?

- @nestjs/config provides a centralized way to load and access environment variables in a NestJS application. It loads values from .env files and provides ConfigService, which allows application components to access configuration values without directly accessing process.env throughout the codebase. This makes configuration easier to manage and change between environments.

2. Why should secrets such as API keys and database passwords never be stored in source code?

- Secrets stored in source code can accidentally be committed to Github and being revealed to other developers that don't have appropriate permission. Once a secret has been committed to a repository, removing the file does not necessarily remove it from the repository’s history. Environment variables and dedicated secret-management systems provide a safer way to supply sensitive configuration to an application.

3. How can you validate environment variables before the app starts?

- NestJS’s ConfigModule can use a validation library such as Joi to define the required environment variables and their expected types. For example, database credentials can be marked as required and ports can be validated as numbers. If a required variable is missing or invalid, the application can fail during startup rather than running with an incorrect configuration.

4. How can you separate configuration for different environments?

- Different environments can use different environment variables or configuration files. For example, development can use a local .env file while production can provide configuration through deployment environment variables or a secret-management service. The application code remains the same while the configuration changes depending on the environment.