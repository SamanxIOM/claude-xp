---
name: respawn
description: Reset every repo in the folder to its default branch
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


# RESPAWN | LOCAL | Reset Branch to Default Branch

- Go through each repo

- Before syncing, note the commit the local default branch is on.

- If the repo has uncommitted code, save it to a "save-point" branch, and stage, commit, sync to remote.

- Switch each repo to the default branch.

- Sync the default branch from remote.

- Create a table named the same name as this step. Show it as a plain markdown table.

  - Repo name

  - Changes - PR link. "Changes" means the difference between the local default branch before the sync and after the sync.

  - Changes - Who

  - Save-point branches

- Give each change its own row. Never put more than one change in a row.

- If a repo has no changes, still show one row for it, with "no changes" in the changes columns.