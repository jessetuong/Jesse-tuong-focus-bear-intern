## What does the coverage bar track, and why is it important?
It tracks how much of the code is executed by the test suite, broken into four
metrics: statements, branches, functions, and lines. It's a fast, objective
signal for how much of the codebase has any test exercising it, so reviewers
can spot code that ships completely unverified.

## Why does Focus Bear enforce a minimum test coverage threshold?
A shared minimum (80%) stops coverage from silently eroding as the code grows,
makes "did you test this?" a build check instead of a review argument, and keeps
critical backend paths from reaching production with zero tests.

## How can high test coverage still lead to untested functionality?
Coverage only records that a line *ran*, not that anything was *checked*. A test
with no assertions (or only `expect(x).toBeDefined()`) executes the code and
counts as covered while verifying almost nothing. Branches, error paths, and
specific return values can all be "covered" yet effectively untested.

## Examples of weak vs. strong test assertions
- Weak: `expect(result).toBeDefined()`, `expect(fn).not.toThrow()`, snapshotting
  a huge object nobody reads.
- Strong: `expect(result).toEqual(expectedObject)`, `expect(repo.save)
  .toHaveBeenCalledWith(expectedArg)`, `await expect(fn()).rejects
  .toBeInstanceOf(NotFoundException)`.

## How can you balance increasing coverage with writing effective tests?
Write tests for behaviour first — each success path, each failure path, each
branch — and let coverage confirm you didn't miss a case, rather than writing
tests just to turn a number green. Use the coverage report as a checklist of
"what haven't I thought about", not as the goal itself.