## How @nestjs/typeorm simplifies database interactions

- Wraps TypeORM as a NestJS module, letting you inject repositories directly into services via NestJS's dependency injection (@InjectRepository()), instead of manually managing a raw connection
- Handles database connection setup
- Lets you define entities as TypeScript classes with decorators (@Entity, @Column), so your database schema and your code models stay connected
- Provides built-in query methods (find, save, delete, etc.) so you rarely need to write raw SQL for common operations

## Entity vs. repository

- Entity: a TypeScript class representing a database table — each instance maps to a row, and its decorated properties map to columns
- Repository: an object that provides methods to interact with a specific entity's table (find, save, update, delete, custom queries) — it's the interface you actually use to read/write data, while the entity just defines the shape of that data

## How TypeORM handles migrations

- Migrations are TypeScript/JS files describing incremental schema changes (create table, add column, etc.), each with an up() (apply) and down() (revert) method
- You generate them via CLI, either automatically by comparing entities to the current DB schema (typeorm migration:generate) or manually (typeorm migration:create)
- Running typeorm migration:run applies pending migrations in order; migration:revert rolls back the last one
- This keeps schema changes version-controlled and reproducible across environments, rather than relying on manual DB edits or synchronize: true (which is fine for local dev but risky in production since it can silently alter/drop data)

## Advantages of PostgreSQL over other databases in a NestJS app

- Strong support for complex queries, joins, and transactions — fits well with TypeORM's relational model
- Rich data types (JSONB, arrays, UUID) that can store semi-structured data without leaving the relational model
-Mature, open-source, well-documented, with strong community/tooling support 
- ACID-compliant, ensuring reliable transactions — important for data integrity in apps handling sensitive data (e.g., user habits, payments)
- Compared to MySQL: generally considered better standards compliance and more advanced features (window functions, full-text search); compared to MongoDB: better fit when data is naturally relational rather than document-based