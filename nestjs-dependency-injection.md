## How dependency injection improves maintainability

- Classes don't create their own dependencies — they receive them from outside (via constructor), so classes stay decoupled from specific implementations
- Makes swapping tools or stack easy (for example, swap a real database service for a mock in tests) without touching the class itself
- Centralizes object creation/wiring in one place (the DI container), instead of scattering new SomeService() calls throughout the codebase
- Makes unit testing far easier — you can inject mock/stub dependencies instead of real ones

## Purpose of @Injectable()

- Marks a class as one that can be managed by NestJS's dependency injection container — it tells Nest "this class can be injected into other classes, and can itself receive injected dependencies"
Without it, Nest won't know how to instantiate the class or resolve its own constructor dependencies
- Commonly used on services, but can apply to any provider (guards, interceptors, etc.)

## Provider scopes in NestJS

- DEFAULT (Singleton) — one instance shared across the entire application lifetime; used for most services (stateless, shared logic, DB connections) — best performance since it's created once
REQUEST — a new instance is created for each incoming request; used when you need per-request state (e.g., tracking request-specific data like a user's tenant ID)
- TRANSIENT — a new instance is created every time the provider is injected anywhere; used when you specifically need isolated, non-shared state per consumer (rare, since it can hurt performance if overused)

## How NestJS automatically resolves dependencies

- Nest reads a class's constructor parameter types (via TypeScript's type metadata/reflection) and looks up matching providers registered in the module
- It builds a dependency graph at startup, resolving each provider's own dependencies recursively before injecting them
- As long as a provider is declared in the module's providers array (or imported via another module's exports), Nest wires it in automatically — no manual instantiation needed