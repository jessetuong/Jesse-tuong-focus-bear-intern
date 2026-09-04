# Introduction to Testing in NestJS — Reflection

## Key differences between unit, integration, and E2E tests
- **Unit:** one class in isolation, every dependency mocked. Fast, numerous, pinpoint failures.
  Example: `UsersService` with a fake repository.
- **Integration:** several real units wired together (often with a real or in-memory DB),
  but not the HTTP layer. Checks that the pieces collaborate correctly.
- **E2E:** the whole app is booted and real HTTP requests hit real routes via Supertest,
  going through guards, pipes, and the database. Slow, few, highest confidence.

## Why testing is important for a NestJS backend
- Prevents regressions as the codebase and team grow — a green suite makes refactors and
  dependency upgrades safe.
- Encodes expected behaviour (validation, auth, status codes) so it's re-checked on every
  change in CI.
- Catches dependency-injection and wiring mistakes early.
- Backend bugs are expensive: they corrupt data or break every client at once.

## How NestJS uses @nestjs/testing to simplify testing
- `Test.createTestingModule({...})` builds a real Nest DI container from a module-like
  definition, so components are tested exactly as they're wired in the app.
- `.overrideProvider(X).useValue(mock)` / `.overrideGuard(...)` swap out the DB, queues, or
  external services without touching production code.
- `.compile()` then `module.get(Token)` pulls out any provider to test.
- `.createNestApplication()` boots a full app instance for E2E tests with Supertest.

## Challenges of writing tests for a NestJS application
- Heavy DI: a missing provider means verbose mock setup, and deciding what to mock vs keep real.
- Everything is async — you must await and clean up between tests.
- Integration/E2E need a disposable database with migrations, seeding, and isolation per test.
- TypeORM repositories and query builders are awkward to mock.
- E2E tests are slow and can be flaky (ports, Redis/Bull, external calls).
- Over-mocking produces tests that pass without verifying anything real.