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
  real credentials tokens.


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
