# Git experience:
- On the main branch, I changed a line to "Jesse has 46 apples" while on another branch, I changed that line to "Jesse has 45 apples", so when I merged them together, it caused to conflictts because Git didn't know which version it should keep.
- I resolved it on GitHub website by reviewing the Pull Request and decided to keep the version on main branch by clicking "Keep the incoming change".
- In thsi exercise, I learned how to switch between 2 branches, create pull request, and resolve merge conflicts by using GitHub website.

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
- Discussion threads show maintainers asking for justification/benchmarks before approving bigger changes
- Even small PRs can take multiple rounds of revision before mergingg