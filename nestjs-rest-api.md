## What is the role of a controller in NestJS?

A controller handles incoming HTTP requests and passes them to appropriate application logic handle functions. It defines routes using decorators such as @Get(), @Post(), @Put(), and @Delete(), extracts request data and returns responses.

## How should business logic be separated from the controller?

Business logic should be placed in services rather than directly inside controllers. The controller should focus mainly on handling HTTP requests and passing operations to the appropriate service.

## Why use services instead of handling logic inside controllers?

Services keep controllers small, focused and also reusable, testable and easier to maintain. This separation also prevents controllers from becoming tightly coupled to application or database logic.

## How does NestJS automatically map request methods to handlers?

NestJS uses decorators such as @Get(), @Post(), @Put() and @Delete() to associate controller methods with HTTP methods. The @Controller('users') decorator establishes the route for the API endpoint, while decorators such as @Get(':id') define the specific route and parameters.