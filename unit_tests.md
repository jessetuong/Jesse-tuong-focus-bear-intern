# Unit Tests — Reflection

## Why is it important to mock API calls in tests?

- Tests run with no real network, so they never fail
  because of latency or rate limits
- Mocking lets us test our own code (loading state, rendering,
  error handling, data mapping) instead of relying on the server
- We control the exact response, so we can reproduce
  hard-to-hit cases on demand: a 500 error, an empty list, malformed JSON, a
  slow response.
- Tests don't create real records, spend API quota, or need
  real credentials tokens - it won't affect the real project.


## What are some common pitfalls when testing asynchronous code?

- **Not awaiting the result.** Assertions run before the promise resolves, so the
  test passes (or fails) for the wrong reason. Use `await screen.findBy...`,
  `await waitFor(...)`, or `await expect(promise).resolves/.rejects`.
- **Leaking mocks between tests.** A mock configured in one test still applies in
  the next. Reset with `jest.restoreAllMocks()` / `jest.clearAllMocks()` in
  `afterEach` / `beforeEach`.
- **`act(...)` warnings.** A state update lands after the test has moved on.
  Usually fixed by awaiting the async query that waits for the update.
- **Testing implementation instead of behaviour.** Asserting only that `fetch`
  was called, rather than that the user actually sees the data or the error
  message.
- **Silent error paths.** An unhandled promise rejection can make a broken test
  look green. Assert the error UI (or the thrown error) explicitly.
- **Mocking at the wrong seam.** Mocking `global.fetch` when the component talks
  to it through a helper module (or vice versa), so the mock never takes effect.

## Why is automated testing important in software development?

- It catches regressions automatically as the code changes, makes it safe when developers want to update anything, documents how code is meant to behave, and gives fast feedback in CI so changes can be verified automatically without the need of human interactions. 

## What did you find challenging when writing your first Jest test?

- Mostly the dependency injection: you can't just `new` a NestJS service in a test,
you build a testing module and provide every dependency — and the TypeORM repo
needs `getRepositoryToken(User)`, not the plain `Repository` class. Also
remembering to `await` the `.rejects` / `.resolves` assertions, and a tooling
error where Jest couldn't parse `@nestjs/bullmq` because it ships as ES modules. Later, I had to 
delete the whole controller.specs because of that bullmq issue.
