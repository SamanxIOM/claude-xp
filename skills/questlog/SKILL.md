---
name: questlog
description: Count blocked, unblocked and total open issues in every repo
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


# QUEST LOG | Work To Do

- Go through each repo

- Check all the open issues.

- An issue is blocked if it has a label containing "blocked", or if GitHub shows it as blocked by another open issue (issue dependencies). Every other open issue is unblocked.

- Create a table named the same name as this step. Show it as a plain markdown table.
  - Repo name
  - Total Blocked Issues
  - Total Unblocked Issues
  - Total Issues
  - End the table with a "Total" row that sums the blocked, unblocked and total columns across all repos