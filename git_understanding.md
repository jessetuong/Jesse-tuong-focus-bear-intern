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

## What suprised me while testing

- cherry-pick can cause conflicts if the target branch has diverged, just like a merge — it's not always clean
- checkout -- <file> silently overwrites uncommitted changes to that file with no undo, which feels riskier once you've tried it
- blame output can point to a large refactor/formatting commit rather than the "real" author, if the file was reformatted at some point

# Branching and Team collaboration:

## Why pushing directly to main is problematic

- Skip the review step, which makes bugs or mistakes in the brnach go straight into main codebase and other teammates can not validate that.
- No safety net — if something breaks, it's already live for the whole team
- No history of why a change happened (no PR discussion trail)
- The mistake of one person will go straight into the main codebase and affect the whole team's progress

## How branches help with reviewing code

- Changes in one person's work remain isolated, which allows them to keep working on their problem while the main codebase/progress remain unchanged.
- Let teammates review a PR before it merges, catching bugs/style issues early
- If a branch failed, the team could simply discard the branch without affecting the main progress

## If two people edit the same file on different branches

- Each can work independently without affecting the other
- When one branch merges first, it's fine
- When the second branch merges, Git tries to auto-merge; if both touched the same lines, it results in a merge conflict that has to be manually resolved before the merge completes — if they touched different lines/parts of the file, Git usually merges both changes automatically

# Git concepts: staging and committing:

## Staging vs. committing

- Staging (git add) — marks changes you made and want to save in the next commit. It acts as a holding area, nothing is saved to history yet. 
- Committing (git commit) — actually saves the staged changes as a permanent snapshot in your repo's history

## Why Git separates these steps

- Lets you build a commit deliberately — you might edit 5 files but only want 2 of them in this commit. For example, you refined a few parts in your index.html file, and fixed a few parts in your javascript files. You just want to commit changes in index.html now and name it accordingly, and then commit the changes in javascript file later. By building commits deliberately like this, you can easily go back and track errors by using git log and git checkout later.
- Moreover, it enables partial commits — even within one file, you can stage only certain changes (git add -p)

## When you'd stage without committing

- You've made several unrelated changes and want to commit them separately with distinct messages (e.g., a bug fix and a typo fix in different files)
- You want to review your changes one more time before finalizing the commit
- You're mid-task and want to "checkpoint" what's ready without yet writing a commit message