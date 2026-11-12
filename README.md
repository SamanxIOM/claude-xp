# claude-xp

`xp` is a Claude Code plugin with a small set of game-themed git workflow skills. This repo offers that one plugin and nothing else.

Version: 1.0.0

## Skills

| Skill | What it does |
| --- | --- |
| `/xp:newgame` | Prepares a fresh repo: moves you onto a `newgame` branch, adds a baseline to `.gitignore`, creates `README.md` and `CLAUDE.md` if missing, and adds `src` and `docs` folders. |
| `/xp:checkpoint` | Commits and pushes your current work. No pull request. |
| `/xp:speedrun` | Commits, pushes, opens a pull request, and sets it to squash and auto-merge. |
| `/xp:finalboss` | Commits, pushes, and opens a pull request that does not auto-merge. |
| `/xp:respawn` | Tidies every repo in the folder back to its default branch, deletes local and remote branches whose pull request has merged, and summarises the remaining branches, pull requests and issues. |

The skills only run when you type them. Claude will not start them on its own.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [git](https://git-scm.com/)
- The [GitHub CLI](https://cli.github.com/) (`gh`), signed in with `gh auth login`

## Install

The commands are the same on every system. Only the terminal you run them in changes.

### Install on Windows

Open PowerShell and run:

```powershell
claude plugin marketplace add SamanxIOM/claude-xp
```

```powershell
claude plugin install xp@claude-xp
```

### Install on Mac

Open Terminal and run:

```bash
claude plugin marketplace add SamanxIOM/claude-xp
```

```bash
claude plugin install xp@claude-xp
```

### Install on Linux

Open your terminal and run:

```bash
claude plugin marketplace add SamanxIOM/claude-xp
```

```bash
claude plugin install xp@claude-xp
```

Restart Claude Code after installing. The skills then show up as `/xp:newgame`, `/xp:checkpoint`, and so on.

You can also install from inside Claude Code on any system:

```
/plugin marketplace add SamanxIOM/claude-xp
/plugin install xp@claude-xp
```

## Uninstall

### Uninstall on Windows

Open PowerShell and run:

```powershell
claude plugin uninstall xp@claude-xp
```

```powershell
claude plugin marketplace remove claude-xp
```

### Uninstall on Mac

Open Terminal and run:

```bash
claude plugin uninstall xp@claude-xp
```

```bash
claude plugin marketplace remove claude-xp
```

### Uninstall on Linux

Open your terminal and run:

```bash
claude plugin uninstall xp@claude-xp
```

```bash
claude plugin marketplace remove claude-xp
```

Restart Claude Code after uninstalling.

## Update

```bash
claude plugin marketplace update claude-xp
```

```bash
claude plugin update xp@claude-xp
```

## License

MIT. See [LICENSE](LICENSE).
