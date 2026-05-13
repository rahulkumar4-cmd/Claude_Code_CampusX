# git-sync

Interactive git workflow with safety checks: fetch, status review, pull, stage, commit, and push.

## Usage

```
/git-sync
```

## What it does

1. **Checks repository state** — fetches from remote, shows branch status, detects conflicts
2. **Pulls latest code** — if behind remote (uses merge strategy)
3. **Interactive staging** — select which files to stage for commit
4. **Commits changes** — prompts for commit message
5. **Pushes to remote** — with confirmation and safety checks

Each step requires explicit permission. Handles merge conflicts, diverged branches, and network errors gracefully. Never force-pushes.

## Implementation

Execute the bash script at `.claude/commands/git-sync`:

```bash
bash .claude/commands/git-sync
```

The script is interactive and will prompt for confirmations at each phase.
