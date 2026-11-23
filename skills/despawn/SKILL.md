---
name: despawn
description: 
disable-model-invocation: true
model: 
effort: 
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

