---
name: finalboss
description: Commit and push current work | Create a Pull Request | Do not auto-merge
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

- If the branch has no commits that are not on the repo's default branch, say so and stop.

- If the branch already has an open PR, do not create another one. The push updates the existing PR. Otherwise, create a PR.

- The PR must not auto-merge.

- After the PR opens, watch its CI checks until they finish. If a check fails because of the code, fix it on the same branch, commit, and push to the same PR, then wait for the checks to run again. Repeat until they pass. Never open a new branch or PR for a CI fix, as one PR per piece of work saves the trees. If a failure is not a code problem (e.g. infrastructure, permissions, or secrets), stop and report it instead.

- If any GitHub issues are linked to this work, reference them in the PR body using GitHub's close-keyword syntax (`Closes #N`, `Fixes #N`, or `Resolves #N`) so that merging the PR automatically closes those issues too. If the PR already existed, add any missing references to its body.

- Do not offer to include a test plan.
