# Git experience:
- On the main branch, I changed a line to "Jesse has 46 apples" while on another branch, I changed that line to "Jesse has 45 apples", so when I merged them together, it caused to conflictts because Git didn't know which version it should keep.
- I resolved it on GitHub website by reviewing the Pull Request and decided to keep the version on main branch by clicking "Keep the incoming change".
- In this exercise, I learned how to switch between 2 branches, create pull request, and resolve merge conflicts by using GitHub website.

## Why PRs are important in a team workflow

- Give teammates details of changes in the branched codebase before they hit the main codebase.
- Create a checkpoint for code review, catching bugs/style issues before merge
- Provide a discussion thread tied to the change, documenting why decisions were made
- Prevent one person from silently breaking main for everyone else

## What makes a well-structured PR

- Clear, specific title (what changed, not just "fix bug")
- Detailed descriptions of what was changed, written in a style that other teammates can understand
- Passes CI/tests before requesting review
- Includes screenshots/notes if it's a UI change

## What you'd likely learn from reviewing an open-source PR (e.g., React)

- Reviewers often push back on edge cases or missing tests, not just style
- Discussion threads show maintainers asking for justification/benchmarks before approving bigger changes.
- Even small PRs can take multiple rounds of revision before merging.

## What makes a good commit message

- Short summary line (~50 chars), imperative mood ("Add", not "Added"), have an brief description of what has changed.
- Explains why, not just what, when it's not obvious
- One logical change per commit

## How it helps team collaboration

- Lets teammates understand history without reading every diff
- Makes git blame/git log actually useful for tracing bugs
- Speeds up code review and onboarding

## How poor messages cause issues later

- Wastes time digging through diffs to figure out what/why
- Makes bug hunting (bisecting) much harder
- Erodes trust in the commit history as documentation

# Git bisect:

- What it does: defines the commit that introduced a bug via binary search through history combining with user's manual checks.

- When to use it in real debugging: when a bug appears but you don't know when it was first appeared and how (such as a function worked last week, but after a few commits in the past week, it is broken). It's especially useful in large repos with hundreds of commits where the bug's origin isn't obvious from recent changes alone.

- Comparing to manually reviewing commits: manual review is linear (check every commit one by one) and slow in a large history; bisect is logarithmic — for 100 commits, manual review could take 100 checks, bisect takes about 7.

# Advanced Git commands:

## What each command does

- git checkout main -- <file> — pulls just one file's content from main into your current branch, without touching anything else you've changed
- git cherry-pick <commit> — copies a single specific commit's changes onto your current branch, without merging the whole source branch
- git log — shows the commit history (hash, author, date, message), so you can trace how the project evolved
- git blame <file> — shows, line by line, which commit and author last changed each line

## When you'd use them in a real project

- checkout -- <file>: you've messed up one file mid-experiment and just want to reset it back to main's version without losing other unrelated work
- cherry-pick: a critical bug fix landed on another branch and you need it on main immediately, without pulling in that branch's other unfinished work
- log: tracing when/why a feature was added, or reviewing what changed before a release
- blame: tracking down who to ask about a confusing line of code, or finding which commit introduced a bug (often paired with bisect)

## What's likely to surprise you while testing (things to watch for)

- cherry-pick can cause conflicts if the target branch has diverged, just like a merge — it's not always clean
- checkout -- <file> silently overwrites uncommitted changes to that file with no undo, which feels riskier once you've tried it
- blame output can point to a large refactor/formatting commit rather than the "real" author, if the file was reformatted at some point