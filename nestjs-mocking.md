# Mocking Dependencies & Database Interactions — Reflection

## Why is mocking important in unit tests?
It isolates the unit under test from slow, unreliable, or stateful things such as a
database, a queue,.. so tests run fast, produce the same result
every time, and a failure points to the code you're actually testing, not
the aplication's error

## How do you mock a NestJS provider (e.g., a service in a controller test)?
Register a fake under the same DI token the real class would use:
`{ provide: UsersService, useValue: fakeUsersService } `inside
`Test.createTestingModule({ providers: [...] })`. Nest's DI hands the controller
your fake instead of building the real service, with no code changes to the
controller itself.

## What are the benefits of mocking the database instead of using a real one?
No DB to provision, migrate, or seed for tests to run; no shared state between
test runs causing flakiness; tests run in milliseconds instead of hitting a
network/disk; plus, you can simulate cases a real DB won't easily give
you — a duplicate key, a timeout, a missing row.

## How do you decide what to mock vs. what to test directly?
Mock anything that crosses a boundary you don't own or that's slow/non-
deterministic/has side effects: the database, external APIs, queues, the clock,
randomness. Things not to mock: the unit you're actually verifying and
its own branching logic.