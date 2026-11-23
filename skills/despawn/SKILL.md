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

- If a local branch's PR has merged, delete the local branch, whoever owned the PR. Local branches are only on this machine, so removing them affects no one else.

- If a local branch has no merged PR, leave it.

- If a local branch has commits that are not on GitHub, leave it, even if its PR has merged, so no work is lost.

- If a remote branch's PR has merged, and the PR was owned by the current user, delete the remote branch. Leave other people's remote branches alone.

- If a remote branch has no merged PR, leave it.

- A PR counts as merged only when GitHub shows it as merged and its base branch is the default branch.

- Never delete the repo's default branch.

- Create a table named the same name as this step. Show it as a plain markdown table.

  - Repo name

  - Local + Remote branch name

  - Local branch status (none / remains / deleted)

  - Remote branch status (none / remains / deleted)

  - PR Link

  - PR Owner