---
name: despawn
description: Delete the current user's merged branches, local and remote
disable-model-invocation: true
model: sonnet
effort: medium
---

# How to run

Run the steps below yourself, in the main chat. Do not delegate to a subagent.


# Prelim Step

- Review the current folder.
  - If the current folder is one repo, review the one repo.
  - If the current folder is not a repo, search all its subfolders, at any depth, for repos, and review every repo found. A repo is a folder that contains a `.git` folder or file.
  - If there are no repos, stop, and say so.
  - Once a repo is found, do not search inside it for more repos.
  - Do not search inside `node_modules` folders.


# DESPAWN | LOCAL & REMOTE | Merged Branches Deleted

- Note the user/username of the current user.

- Go through each repo

- Check what local branches there are

- Check what remote branches there are

- If the local branch has no remote branch, leave it, unless its PR was owned by the current user and has merged. Then delete the local branch.

- If a remote branch has no local branch, leave it.

- If the local branch or remote branch has been merged into the default branch, and the PR was owned by the current user, it is therefore no longer needed. Delete the local branch and/or remote branch of merged PRs only.

- Never delete the repo's default branch.

- Create a table named the same name as this step. Show it as a plain markdown table.

  - Repo name

  - Local + Remote branch name

  - Local branch deleted (yes / no)

  - Remote branch deleted (yes / no / already gone)

  - PR Link