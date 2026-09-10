# When to Use Google, AI, or Ask for Help — Reflection

## When do I prefer AI vs. searching Google?
I use Google (and official docs) when I know the concept and need something
specific and authoritative: exact API signatures, a config option, what an error
code means, or anything version-sensitive where a wrong answer wastes hours.

I use AI when the problem is open-ended or explanatory: understanding an
unfamiliar error, drafting boilerplate or a test, comparing a few possible
approaches, or getting unstuck on a generic bug. I treat its output as a starting
point and verify anything load-bearing against the docs, because it's confidently
wrong on details and doesn't know our codebase.

## How do I decide when to ask a colleague instead?
I ask a person when: the problem touches internal systems, secrets, or customer
data (can't go in a public tool); it's a decision about our conventions or
architecture (no external source knows our context); it's blocking other people
or production; or I've timeboxed ~30–45 minutes with no real progress. When I
ask, I bring what I tried, what I expected, and what actually happened.

## What challenges do developers face when troubleshooting alone?
Tunnel vision on the first hypothesis, not noticing a wrong assumption, no one to
catch an obvious mistake, and losing track of time. It's also easy to over-trust
a Google or AI answer that looks plausible but doesn't fit the situation, and to
keep grinding past the point where asking would have been faster.