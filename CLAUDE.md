# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Spendly** — a Flask + SQLite expense-tracker web app used as a learning project. Routes, the database layer, and frontend JS are intentionally stubbed out; students implement them step by step.

## Commands

Dependencies are managed with `uv` (lockfile: `uv.lock`). Python version is pinned in `.python-version` (3.11).

```bash
# Install dependencies and activate venv
uv sync
source .venv/bin/activate

# Run the dev server (port 5001)
flask --app app run --debug
# or
python app.py

# Run tests
pytest

# Run a single test file or test
pytest tests/test_foo.py
pytest tests/test_foo.py::test_bar

# Git workflow (interactive sync command)
/git-sync
```

## Custom Commands

This project has a custom `/git-sync` command that provides an interactive, safe git workflow:

1. **Checks repository state** — fetches from remote, shows status, detects conflicts
2. **Pulls latest code** — if behind remote (uses merge strategy)
3. **Interactive staging** — select which files to stage for commit
4. **Commits changes** — prompts for commit message
5. **Pushes to remote** — with confirmation and safety checks

Each step requires explicit permission. The command handles merge conflicts, diverged branches, and network errors gracefully. Never force-pushes.

## Architecture

```
app.py            — Flask application, all route definitions
database/
  __init__.py     — empty
  db.py           — stub: get_db(), init_db(), seed_db() (students implement in Step 1)
templates/
  base.html       — shared layout: navbar, footer, Google Fonts (DM Serif Display, DM Sans)
  landing.html    — public landing page (extends base.html)
  login.html / register.html — auth pages (extends base.html)
  terms.html / privacy.html  — static legal pages
static/
  css/style.css   — main stylesheet
  css/landing.css — landing-page-specific styles
  js/main.js      — stub, students add JS here per step
```

**Data layer:** SQLite via `database/db.py`. `get_db()` is expected to return a connection with `row_factory = sqlite3.Row` and `PRAGMA foreign_keys = ON`. The database file is not committed; `init_db()` / `seed_db()` create and populate it on first run.

**Stub routes** in `app.py` (`/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`) return placeholder strings — these are the implementation targets for later steps.
