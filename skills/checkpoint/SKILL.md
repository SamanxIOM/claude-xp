---
name: checkpoint
description: Commit and push current work
disable-model-invocation: true
---

# How to run

Run the steps below yourself, in the main chat. Do not delegate to a subagent.

# Task

- If the user is on a branch other than the repo's default branch, check if the remote branch has been deleted after its PR was merged. If so, it's a stale local branch. Switch to the repo's default branch and sync it from the remote, then continue with the next step. Don't lose any uncommitted code (staged or unstaged).

- If the user is on the repo's default branch, create a new local branch. Follow standard GitHub conventions (e.g. `feat/…`, `fix/…`, `chore/…`, `docs/…`).

- Stage, commit, and push the current local branch to the remote branch.

- If nothing was committed or pushed, say so and stop.

- If any GitHub issues are linked to this work, reference them in the commit message using GitHub's close-keyword syntax (`Closes #N`, `Fixes #N`, or `Resolves #N`) so that those issues close automatically once the commit reaches the repo's default branch.

- Do not offer to make a PR. It is common for the user to run this skill to save their work before continuing with more work.

- Do not offer to include a test plan.
