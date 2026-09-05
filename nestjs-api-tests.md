# Jest & Supertest API Testing — Reflection

## How does Supertest help test API endpoints?
It fires real HTTP requests at a running Nest app instance (via
`app.getHttpServer()`) and lets you assert on the actual response — status code,
body, headers — the same way a real client would see it. It exercises the whole
request pipeline: routing, pipes, guards, and controller/service code together.

## What is the difference between unit tests and API tests?
A unit test isolates one class with everything else mocked — fast, pinpoints
exactly which function is broken. An API (integration/e2e) test boots the real
app and a real database and checks the system as a whole behaves correctly from
the outside — slower, but it's the only kind of test that catches wiring bugs
like a route registered in the wrong order or a guard not applied.

## Why should authentication be mocked in integration tests?
So the test verifies your endpoint's behavior, not the JWT library's. Signing
and verifying real tokens for every test adds setup, secret management, and
flakiness that has nothing to do with what the endpoint does once a user is
authenticated. Overriding the guard lets you simulate "authenticated as an
admin" or "unauthenticated" instantly and deterministically.

## How can you structure API tests to cover both success and failure cases?
For each endpoint, write at least one happy-path test (valid input → expected
status/body) and one failure test per failure mode: invalid input (400),
missing/invalid auth (401/403), not-found (404). Group them by endpoint in
`describe` blocks so the success and failure cases for the same route sit next
to each other.