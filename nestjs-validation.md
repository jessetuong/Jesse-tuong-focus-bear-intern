## What is the purpose of pipes in NestJS?

Pipes are used to transform and validate incoming request data before it reaches the controller handler. They can ensure that data has the correct format or convert data into the required type.

## How does ValidationPipe improve API security and data integrity?

ValidationPipe validates incoming data against DTO rules before it reaches the application’s business logic. This prevents unexpected or faulty data from being processed. Options such as whitelist and forbidNonWhitelisted can also prevent clients from sending properties that aren’t part of the API’s expected data structure.

## What is the difference between built-in and custom pipes?

Built-in pipes are provided by NestJS for common validation and transformation tasks, such as ValidationPipe and ParseIntPipe. Custom pipes are created by developers when they need extra requirements of logic they want to check.

## How do decorators like @IsString() and @IsNumber() work with DTOs?

Decorators from class-validator attach validation rules to DTO properties. When a DTO is processed by ValidationPipe, these rules are checked against the incoming request data. For example, @IsString() requires a property to contain a string, while @IsNumber() requires it to contain a number. If validation fails, NestJS automatically returns a 400 Bad Request response.