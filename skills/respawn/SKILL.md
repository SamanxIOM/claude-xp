---
name: respawn
description: Tidy every repo in the folder
disable-model-invocation: true
---

# Models

- Run the steps below by delegating to an Agent subagent. Claude should determine which model and effort is best to use.
- If the work can be split into independent parts, e.g. one part per repo, use multiple subagents running in parallel, and use a workflow if workflows are available. Only one subagent may change any one repo at a time.
- The subagent cannot see this conversation. In its prompt, include anything it needs from it, such as a short summary of the work being saved and any GitHub issue numbers linked to it.
- When it finishes, return to the main session and report the result.

# Tables

Show each table as its own inline widget, so there are five separate widgets, one per table. Never combine tables into one widget, and never put two tables in the same widget. Show them in this order: `RETURN TO SPAWN`, `DESPAWN`, `INVENTORY CHECK` for the current user, `INVENTORY CHECK` for other users, then `QUEST LOG`. Each widget holds its four name labels followed by its table.

Every table must show every repo, each with its own row and its own repo name. Never group repos together or summarise them in one row (for example "all repos"), even when they all have the same result. If a repo has nothing to report in a table, still show a row for it, e.g. "nothing to delete" or "none".

Above each table, show its name as four labels in a row. For example, the name `RETURN TO SPAWN | LOCAL | Reset Branch to Default Branch | CURRENT USER` is shown as:

- The game name, `RETURN TO SPAWN`, as a small blue label. Keep it in capitals. The other game names are `DESPAWN`, `INVENTORY CHECK` and `QUEST LOG`.
- The scope, `LOCAL`, as a small yellow label. Keep it in capitals. The other scopes are `LOCAL & REMOTE` and `REMOTE`.
- The description, `Reset Branch to Default Branch`, as a small green label. It says what the table does.
- The users, `CURRENT USER`, as a small red label. Keep it in capitals. It says whose work the table shows. The other users labels are `OTHER USERS` and `ALL USERS`.

Do not show the vertical bars (`|`) between the labels.

For each label's colours, use that colour from the widget's own colour palette (blue, amber for yellow, green, red), so it stays readable in both light and dark mode: a pale background with dark text of the same colour in light mode, and a dark background with pale text of the same colour in dark mode.


# Talk

- The tables are the report. Do not write a summary, a recap of the tables, or closing notes before or after them.
- Only write text when something is critical: the skill was paused, a step failed, work could not be saved, or a deletion failed. Keep it to what happened and which repo.
- If nothing is critical, show the tables and nothing else.


# Prelim Step

- If using the Claude desktop app
  - if this is a new session, rename the session to the folder name plus the word "respawn", e.g. "folder-respawn".
  - If this is an existing session, don't rename the session name
- Review the current folder.
  - If the current folder is one repo, review the one repo.
  - If the current folder is not a repo, search all its subfolders, at any depth, for repos, and review every repo found. A repo is a folder that contains a `.git` folder or file.
  - Once a repo is found, do not search inside it for more repos.
  - Do not search inside `node_modules` folders.
- Silently skip any folder that is not a git repo.
- In every table, name each repo by its path from the current folder (e.g. `acme/api/api-gateway`), so repos with the same name in different folders can be told apart.
- In every table, show the repo path with each folder on its own line, so the repo column stays narrow and leaves room for the other columns. Keep the `/` at the end of each folder line. For example, `acme/web/shop-checkout-site` is shown as:

  ```
  acme/
  web/
  shop-checkout-site
  ```

  A repo at the top of the current folder, with no folders in its path, is shown on one line.
- In every table, highlight the last part of the repo path, the repo's own name, in pastel lavender (purple). Only highlight that last line, not the folders above it. In the example above, only `shop-checkout-site` is highlighted. Use the purple from the widget's own colour palette so it stays readable in both light and dark mode: a pale lavender background with dark purple text in light mode, and a dark purple background with pale lavender text in dark mode.
- In every table, alternate the repo highlight between lavender and pink, changing colour each time the repo changes. The first repo in each table is lavender. Rows that belong to the same repo as the row above keep the same colour. When a row shows a different repo, switch to the other colour. For example:

  ```
  row 1  repo A  lavender
  row 2  repo A  lavender
  row 3  repo A  lavender
  row 4  repo B  pink
  row 5  repo B  pink
  row 6  repo C  lavender
  ```

  For pink, use the pink from the widget's own colour palette: a pale pink background with dark pink text in light mode, and a dark pink background with pale pink text in dark mode.
- In the RETURN TO SPAWN, DESPAWN and both INVENTORY CHECK tables (not QUEST LOG), if the repo's own name (the last part of the repo path) is 16 characters or longer, split it in half, once only, onto two lines. If the name has an odd number of characters, the first line gets the extra one. Names under 16 characters stay on one line, and folder names above it are never split. Highlight both lines. For example:

  ```
  12345678901234567890  becomes  1234567890
                                 1234567890

  1234567890123456      becomes  12345678
                                 90123456

  12345678901234567     becomes  123456789
                                 01234567
  ```

  So `shop-checkout-site` is shown as `shop-chec` and `kout-site`. In QUEST LOG the repo's own name is always shown in full on one line.
- Never let a line of a repo path wrap any further than the rules above say. Each folder line and each line of the repo's own name stays whole on its own line, even though other columns wrap (in HTML, set `white-space: nowrap` on each line). Otherwise the browser breaks the name again at hyphens when the column is narrow.
- In every table, split branch names at each `/` the same way as repo paths, both local and remote, including "save-point" branches. The highlight does not apply to branch names: put each part of the name on its own line, breaking after each `/` and keeping the `/` at the end of the line. For example, `chore/gitignore-localhost-dev` is shown as:

  ```
  chore/
  gitignore-localhost-dev
  ```

  A branch name with no `/` is shown on one line.
- In every table, let every column wrap its text, so no column is forced wide and the table fits without squashing. Repo paths are the one exception, see above. A long part of a branch name may still wrap within its own line.
- In every table, make each remote branch name and each PR number a link that opens it on GitHub:
  - A remote branch links to its page, e.g. `https://github.com/<owner>/<repo>/tree/<branch>`.
  - A PR number links to the PR, e.g. `https://github.com/<owner>/<repo>/pull/<number>`.
  - Only link a remote branch that still exists on GitHub. A branch that was deleted or is already gone is shown as plain text, so no link leads to a missing page. A PR is always linked, even when it has merged or closed.
  - Local-only branches, and cells that say "none", are plain text.
- If no repos are found, say so and stop.
- Do a scan/check of all the local branches.
- Do a scan/check of all the remote branches.
- Do a scan/check of all the PRs linked to any local and remote branches.
- Do a scan/check of all the open issues.
- Find the current user's GitHub username (e.g. `gh api user`) to find who the current user is.
- Before changing anything in any repo, check every repo for an awkward state. If any repo is in one, pause the whole skill: change nothing in any repo, tell the user which repo it is and why, and wait for the user to say how to continue. The awkward states are:
  - A merge, rebase, cherry-pick or revert is in progress.
  - The repo is not on any branch (detached HEAD).
  - The repo has no GitHub remote.
  - The GitHub CLI (`gh`) is not installed or not signed in.


# RETURN TO SPAWN | LOCAL | Reset Branch to Default Branch | CURRENT USER

- Go through each repo
- If there is any uncommitted code, first create a branch called "save-point" from the current branch/worktree, then stage, commit and sync the code onto it. Don't have anything stashed in the repo, branch only. If there is already a branch called "save-point", append a number to the new branch name, e.g. "save-point-1".
- When staging for a "save-point" branch, follow the repo's `.gitignore`. Only stage files that git does not ignore, and never force-add an ignored file.
- Then, for any repo not on its default branch, switch to the repo's default branch. Sync it from the GitHub remote.

- Create a table named the same name as this step
  - Repo name
  - What changes have happened on the repo's default branch since this machine last synced it, e.g. deployed xyz. Head this column "Changes on default branch since last sync". Put each change on its own line, always, even when a line holds only a few words. Never join changes on one line with `;` or `,`. Write each line as a brief summary of the change, then ` - `, then the PR number, then ` - `, then the GitHub username of the person who made the change, with a space either side of each dash. The PR number is a link to the PR. If a change has no PR, leave out the PR number and its dash. For example:

    ```
    added Apple Pay at checkout - #41 - jordan-k
    fixed broken image on product page - #43 - priya-dev
    deployed v2.3.0 to production - tomasz-w
    ```
  - There is no separate column for who made the change, as each line already names them.
  - Any "save-point" branches made.


# DESPAWN | LOCAL & REMOTE | Merged Branches Deleted | CURRENT USER

- Go through each repo.
- Check what local branches there are.
- Check what remote branches there are.
- Check what PRs the local and remote branches are linked to, if they are linked.
- This step only looks at the current user's own work. Only branches whose PR was opened by the current user are considered.
- For every branch whose PR has been merged, and whose PR was opened by the current user, delete the local branch and delete the remote branch.
- Never delete or change anything that belongs to another user, not their remote branch and not a local copy of it on this machine. Each person runs respawn on their own machine to tidy their own work. Other users' branches only show in the INVENTORY CHECK table for other users.
- Never delete the repo's default branch.
- Do not delete a local branch that has commits which are not part of the merged PR, as that work would be lost. Leave it, and leave its remote branch, so they show in the INVENTORY CHECK table for the current user.
- If a branch is already gone, or a deletion fails (e.g. the branch is protected), carry on and show that in the table.

- Create a table named the same name as this step, showing only the current user's branches and PRs
  - repo name
  - the branch name
  - the PR summary, then ` - `, then the PR number, with a space either side of the dash, e.g. `add full-text search - #7`. There is no separate PR number column in this table. The PR number is still a link to the PR.
  - local branch: deleted / did not exist / kept, with the reason
  - remote branch: deleted / already gone / failed, with the reason
- There is no owner column in this table, as every row belongs to the current user.
- If nothing was deleted in a repo, show one row for that repo that says "nothing to delete". Every repo gets its own row with its own repo name. Never group repos into one row, and never use "all repos" or similar in place of a repo name.


# INVENTORY CHECK

This step deletes nothing. It shows what is left after the step above, split into two tables: one for the current user's own work, and one for everyone else's work in the same repos.

- Go through each repo.
- Check what local branches there are.
- Check what remote branches there are.
- Check what PRs the local and remote branches are linked to, if they are linked.
- Tie them all together, so each branch shows once, with its local copy, its remote copy and its PRs on the same row. If there are any gaps, show "none".
- Decide who owns each branch:
  - If the branch has a PR, the owner is the person who opened the PR.
  - If it has no PR, the owner is the GitHub user who made the newest commit on the branch that is not on the default branch. If no GitHub user can be found, use the git author name.
  - A local branch with no remote branch (it is only on this machine) belongs to the current user. So do "save-point" branches.
- Never show the repo's default branch (e.g. `main`) in either table, local or remote. Both tables only show branches other than the default branch, as that is where work is in progress.
- Put each branch in exactly one of the two tables below, by its owner.


## INVENTORY CHECK | LOCAL & REMOTE | Branch & PR Overview | CURRENT USER

- Create a table named the same name as this section, for the branches owned by the current user.
  - repo name
  - local branch: "yes" if this machine has a local copy of the branch, or "none" if it does not. Do not repeat the branch name here, as it is the same as the remote branch name.
  - the remote branch name, linked to the branch on GitHub. If the branch is only on this machine and not on GitHub, still show its name here, as plain text with `(only on this machine)` under it, so the branch name is never lost.
  - the PR summary linked to the branch, if there is one, then ` - `, then the PR number, with a space either side of the dash, e.g. `add tags to notes - #9`. The PR number is still a link to the PR. If a branch has more than one PR, put each PR on its own line, always.
  - CI tests passed/failed
  - If auto-merge is enabled/disabled
  - Why it has not merged (if known, otherwise say unknown). If there is no PR, say "no PR".
- There is no owner column in this table, as every row belongs to the current user.
- If a repo has no branches owned by the current user, show one row for that repo that says "no branches of your own". Every repo gets its own row with its own repo name.


## INVENTORY CHECK | LOCAL & REMOTE | Branch & PR Overview | OTHER USERS

- Before making this table, bring every other user's remote branch down to this machine and up to date, so the current user can help with their work:
  - Skip the default branch, and skip any branch whose PR has merged.
  - If this machine has no local copy of the branch, create one that tracks the remote branch.
  - If this machine has a local copy, update it to match the remote branch, but only when that can be done cleanly (a fast-forward). Update it without switching to it, e.g. `git fetch origin <branch>:<branch>`.
  - If the local copy has commits that are not on the remote branch, do not update it and do not change it in any way, so no work is lost. Flag it in the branch column, e.g. `feat/refunds (not updated, has your own commits)`.
  - Never force-update, rebase or reset another user's branch, and never push anything to it.
  - Do not list or summarise the commits that came down. Branches can have many commits, and the current user only needs them to be up to date.
- Create a table named the same name as this section, for the branches owned by anyone other than the current user.
  - repo name
  - the local & remote branch name, in one column headed "Local & remote branch". After the sync above, the local and remote branches have the same name, so one column shows both. The name links to the remote branch. Add a note under the name only when the local copy is not the same as the remote branch:
    - `(no local copy)` for a merged branch this machine does not have.
    - `(not updated, has your own commits)` for a local copy the sync left alone.
  - the PR summary linked to the branch, then ` - `, then the PR number, then ` - `, then the GitHub username of the owner, with a space either side of each dash, e.g. `gift cards at checkout - #36 - jordan-k`. The PR number is still a link to the PR. If a branch has more than one PR, put each PR on its own line, always. If the branch has no PR, show `no PR - ` and the owner, e.g. `no PR - jordan-k`, so the owner is always shown.
  - There is no separate owner column in this table, as the PR summary names the owner.
  - CI tests passed/failed
  - If auto-merge is enabled/disabled
  - Why it has not merged (if known, otherwise say unknown). If there is no PR, say "no PR". If the PR has merged but the remote branch was kept because it belongs to someone else, say "merged, belongs to" and the person's name.
- Sort the rows within each repo by owner, so each person's branches sit together.
- If a repo has no branches owned by other users, show one row for that repo that says "no other users' branches". Every repo gets its own row with its own repo name.


# QUEST LOG | REMOTE | Work To Do | ALL USERS

- Go through each repo
- Check all the open issues.
- An issue is blocked if it has a label containing "blocked", or if GitHub shows it as blocked by another open issue (issue dependencies). Every other open issue is unblocked.

- Create a table named the same name as this step
  - Repo name
  - Total number of issues blocked, assigned to no-one
  - Total number of issues blocked, assigned to someone else
  - Total number of issues blocked, assigned to the current user
  - Total number of issues unblocked, assigned to no-one
  - Total number of issues unblocked, assigned to someone else
  - Total number of issues unblocked, assigned to the current user
  - Total number of issues
  - End the table with a "Total" row that sums the blocked, unblocked and total columns across all repos
- Show a vertical divider line between these pairs of columns, to group the table into repo, blocked, unblocked and total:
  - between the repo name and the blocked, assigned to no-one column
  - between the blocked, assigned to the current user column and the unblocked, assigned to no-one column
  - between the unblocked, assigned to the current user column and the total number of issues column
- Do not show vertical divider lines between any other columns in this table.