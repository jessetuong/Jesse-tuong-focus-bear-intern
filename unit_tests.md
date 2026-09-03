# Unit Tests — Reflection

## Why is it important to mock API calls in tests?
- Fast and reliable: latency, downtime, or rate limits won't affect the test since there is no network required
- Isolated: allow developers to test the component's own logic, not the server. Also, we control the exact response and can easily simulate errors, empty results, or bad data.
- No side effects: tests never create real records, spend API quota, or need real credentials.

## Common pitfalls when testing asynchronous code
- Not awaiting the result: assertions run before the promise resolves. Use `await screen.findBy...` or `waitFor`.
- Previous tests affect the later one: reset with `jest.restoreAllMocks()` so one test doesn't affect the next.
- `act()` warnings: state updates that land after the test moved on — fixed by awaiting the async query.
- Testing implementation instead of behaviour: assert what the user sees, not just that `fetch` was called.
- Silent error paths: an unhandled rejection can make a broken test look green — assert the error UI explicitly.