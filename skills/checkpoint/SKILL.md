---
name: checkpoint
description: Commit and push current work
disable-model-invocation: true
---

# Models

- Run the steps below by delegating to an Agent subagent. Claude should determine which model and effort is best to use.
- If the work can be split into independent parts, e.g. one part per repo, use multiple subagents running in parallel, and use a workflow if workflows are available. Only one subagent may change any one repo at a time.
- The subagent cannot see this conversation. In its prompt, include anything it needs from it, such as a short summary of the work being saved and any GitHub issue numbers linked to it.
- When it finishes, return to the main session and report the result.

# Task

- If the user is on a branch other than the repo's default branch, check if the remote branch has been deleted after its PR was merged. If so, it's a stale local branch. Switch to the repo's default branch and sync it from the remote, then continue with the next step. Don't lose any uncommitted code (staged or unstaged).

- If the user is on the repo's default branch, create a new local branch. Follow standard GitHub conventions (e.g. `feat/…`, `fix/…`, `chore/…`, `docs/…`).

- Stage, commit, and push the current local branch to the remote branch.

- If nothing was committed or pushed, say so and stop.

- If any GitHub issues are linked to this work, reference them in the commit message using GitHub's close-keyword syntax (`Closes #N`, `Fixes #N`, or `Resolves #N`) so that those issues close automatically once the commit reaches the repo's default branch.

- Do not offer to make a PR. It is common for the user to run this skill to save their work before continuing with more work.

- Do not offer to include a test plan.
