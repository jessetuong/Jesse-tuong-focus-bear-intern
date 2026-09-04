# Writing Unit Tests for Services & Controllers — Reflection

## Why is it important to test services separately from controllers?
They have different jobs. Services hold business logic (rules, calculations,
database access); controllers just receive the HTTP request, delegate, and shape
the response. Testing them separately keeps each test focused on one
responsibility, so a failure points to one place, and the controller test doesn't
need a real service or database.

## How does mocking dependencies improve unit testing?
- It isolates the unit under test, so a failure is caused by that class, not a
  collaborator.
- It removes slow or unreliable things (DB, queues, HTTP).
- It lets you force hard-to-reproduce scenarios (repo returns null, service
  throws).
- It lets you assert interactions — e.g. that `save` was called with the right
  arguments.

## Common pitfalls when writing unit tests in NestJS
- Forgetting to provide a dependency (DI resolution error), or providing the real
  one and accidentally hitting the database.
- Not using `getRepositoryToken()` to mock a TypeORM repository.
- Not resetting mocks between tests.
- Missing `await` on `.resolves` / `.rejects` assertions.
- Import-chain problems (a controller pulling in an ESM-only package like
  `@nestjs/bullmq` that Jest can't parse by default).
- Only asserting "should be defined" instead of real behaviour.

## How can you ensure unit tests cover all edge cases?
Test every branch of the method: success, not-found, invalid input, empty
results, thrown errors. Use `jest --coverage` to find untested lines and
branches (as a hint, not a target). Think in input partitions and boundaries
(0 / 1 / many, null/undefined, duplicates). Add a regression test for every bug
you fix.