# Project Guidelines

## Mandatory Development Checklist
Before submitting changes, all items must be completed:

- [ ] Build: `uv sync`
- [ ] Lint: `uv run ruff check .`
- [ ] Test: `uv run pytest`

## Build and Run
Core development commands:

- Run app: `uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000`
- Open app in external browser: `"$BROWSER" http://localhost:8000`

## Architecture
Soc Ops is a FastAPI + Jinja2 + HTMX app with server-side game state.

- `app/main.py`: Routes that return full pages or HTMX component fragments.
- `app/game_service.py`: Session lifecycle and mutable per-user game state.
- `app/game_logic.py`: Pure board generation and bingo detection.
- `app/templates/` and `app/static/`: UI templates and CSS/JS assets.
- `tests/`: API tests in `tests/test_api.py`, logic tests in `tests/test_game_logic.py`.

## Conventions
- Keep rules in `app/game_logic.py` pure; keep request/session concerns in `app/game_service.py`.
- For UI changes, prefer HTMX partial updates by returning component templates from routes.
- Reuse utility classes in `app/static/css/app.css` before adding new styles.
- Follow existing pytest style (`TestClient` fixture and class-based tests).

## Environment Notes
- Do not use VS Code Simple Browser for this project; HTMX interactions should be validated in a full browser.
- In GitHub Codespaces (browser), ensure port `8000` is Public if styles/interactions fail.

## Reference Docs
Link to these docs instead of duplicating content:

- `README.md` (project overview and lab links)
- `workshop/01-setup.md` (setup workflow and troubleshooting)
- `.github/instructions/css-utilities.instructions.md` (available CSS utility classes)
- `.github/instructions/frontend-design.instructions.md` (design direction and anti-generic frontend guidance)
- `.github/instructions/general.instructions.md` (global workspace constraints)
