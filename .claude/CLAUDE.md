# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the app

```bash
python app.py          # starts Flask on http://localhost:5001 (debug mode on)
```

Use a virtual environment (`venv/`) — it is already present. Activate it before running:

```bash
# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

## Running tests

```bash
pytest                        # run all tests
pytest tests/test_foo.py      # run a single test file
pytest -k "test_name"         # run a single test by name
```

Dependencies: `flask`, `werkzeug`, `pytest`, `pytest-flask` (see `requirements.txt`).

## Architecture

This is a **Flask + SQLite** expense tracker built as a step-by-step student project. Much of the backend is intentionally left as stubs for students to implement.

### Request flow

```
Browser → app.py (route) → templates/*.html (Jinja2, extends base.html)
                         → database/db.py (SQLite via get_db())
```

### Key files

| File | Purpose |
|---|---|
| `app.py` | All routes. Implemented routes render templates; stub routes return plain strings |
| `database/db.py` | **Not yet implemented.** Students write `get_db()`, `init_db()`, `seed_db()` here |
| `templates/base.html` | Shared layout: navbar, footer (with Terms/Privacy links), font imports |
| `static/css/style.css` | Global styles — CSS variables (`--ink`, `--accent`, `--paper`, etc.), navbar, auth pages, footer |
| `static/css/landing.css` | Landing-page-only styles (`lp-` prefixed classes). Loaded via `{% block head %}` in `landing.html` |
| `static/js/main.js` | Placeholder — students add JS here as features are built |

### CSS conventions

All CSS variables are defined in `style.css` under `:root`. The key palette:
- `--ink` / `--ink-soft` / `--ink-muted` — text shades (dark → light)
- `--paper` / `--paper-warm` / `--paper-card` — background shades
- `--accent` (`#1a472a`) — primary green; `--accent-2` (`#c17f24`) — amber
- `--font-display`: DM Serif Display (headings); `--font-body`: DM Sans (everything else)

Landing-page components use `lp-` prefixes in `landing.css` to avoid collisions with `style.css`.

### Template structure

All pages extend `base.html`. Available blocks: `title`, `head` (extra `<link>`/`<meta>`), `content`, `scripts`.

### Implemented routes

| Route | Status |
|---|---|
| `GET /` | Landing page |
| `GET /login` | Login form (UI only) |
| `GET /register` | Register form (UI only) |
| `GET /terms` | Terms and Conditions |
| `GET /privacy` | Privacy Policy |
| `GET /refresh` | Redirects to `Referer` or `/` |

### Stub routes (students implement)

`/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`


