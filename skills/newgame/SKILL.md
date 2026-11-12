---
name: newgame
description: Prepare a fresh repo with a gitignore baseline, README, CLAUDE.md and starter folders
disable-model-invocation: true
---

# Models

- Run the steps below by delegating to an Agent subagent. Claude should determine which model and effort is best to use.
- If the work can be split into independent parts, e.g. one part per repo, use multiple subagents running in parallel, and use a workflow if workflows are available. Only one subagent may change any one repo at a time.
- The subagent cannot see this conversation. In its prompt, include anything it needs from it, such as a short summary of the work being saved and any GitHub issue numbers linked to it.
- When it finishes, return to the main session and report the result.

# Task

- If the current folder is not a git repo, say so and stop.

- If the user is on the repo's default branch, switch to a branch called "newgame". If a "newgame" branch already exists, use it. Otherwise, create it.

- If a `.gitignore` file does not already exist at the repo root, create one.

- The block below is made of groups. Each group is a `#` comment line followed by its rule lines, and groups are separated by blank lines.

- For each group, check whether each rule line (any line that is not a comment or blank) is already present in `.gitignore` as an exact whole line.
  - If every rule line in the group is already present, skip the whole group, including its comment.
  - Otherwise, append the group's comment, unless that exact comment line is already present, followed by only the missing rule lines. Do not duplicate lines that are already there.

- Do not ask the user about existing comments or duplicates, and do not suggest cleanup. Just apply the rules above and report what was added and what was skipped.

  ````
  # macOS
  .DS_Store

  # Windows
  Thumbs.db
  desktop.ini

  # Claude Code
  settings.local.json
  CLAUDE.local.md
  .claude/worktrees/

  # Environment
  .env
  .env.*
  !.env.example
  .dev.vars
  .dev.vars.*
  !.dev.vars.example

  # Logs
  *.log

  # Node packages
  node_modules/

  # Wrangler
  .wrangler/

  # Skills (each person's own tool settings and output, never shared)
  .impeccable/
  graphify-out/

  # Media (video and audio renders, too big for git)
  *.mp4
  *.mp3
  *.wav
  ````

- If a `README.md` file does not already exist at the repo root, create one. Its only content is a heading with the repo's name, e.g. `# reponame`. If one already exists, leave it as it is.

- If a `CLAUDE.md` file does not already exist at the repo root, create one with exactly the content below, and nothing else. If one already exists, leave it as it is.

  ````
  # Notes for Claude

  Coming soon.
  ````

- Check each of these folders at the repo root:
  - `src`
  - `docs`

  If a folder already exists, skip it: do not add a `.gitkeep` and do not touch anything inside it. If it does not exist, create it and add an empty `.gitkeep` file, so that git keeps the folder even while it is empty.

- Report which files and folders were created and which were skipped because they already existed.
