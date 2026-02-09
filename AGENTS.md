# Repository Guidelines

## Project Structure & Module Organization
- `src/`: core analysis pipeline and business logic (`core/`, `services/`, `repositories/`).
- `data_provider/`: market data adapters (AkShare, Tushare, YFinance, etc.).
- `api/`: FastAPI backend (`api/v1/endpoints`, `api/v1/schemas`, `middlewares`).
- `bot/`: bot command handlers and platform integrations (Feishu, DingTalk, Discord).
- `apps/dsa-web/`: React + TypeScript frontend (Vite + ESLint).
- `web/`: legacy local WebUI modules.
- `docs/`, `docker/`, `sources/`: documentation, deployment artifacts, and image assets.

## Build, Test, and Development Commands
- `pip install -r requirements.txt`: install Python dependencies.
- `cp .env.example .env`: initialize local environment variables.
- `python main.py --stocks AAPL,TSLA --no-market-review`: run local stock analysis.
- `python main.py --serve-only --host 0.0.0.0 --port 8000`: run FastAPI service only.
- `./test.sh quick`: run a fast end-to-end smoke test.
- `./test.sh syntax` and `./test.sh flake8`: run syntax and critical static checks aligned with CI.
- `cd apps/dsa-web && npm install && npm run dev`: run frontend locally.
- `cd apps/dsa-web && npm run build && npm run lint`: frontend build and lint.
- `docker build -f docker/Dockerfile .`: validate Docker image build.

## Coding Style & Naming Conventions
- Python uses 4-space indentation and PEP 8; max line length is `120`.
- Format/lint with `black`, `isort`, and `flake8` (see `pyproject.toml`, `setup.cfg`).
- Naming: `snake_case` for modules/functions, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants.
- Frontend naming: React components in `PascalCase` (for example, `ReportSummary.tsx`), hooks prefixed with `use`.

## Testing Guidelines
- Pytest is configured in `setup.cfg` with `test_*.py` discovery and verbose output.
- Current validation is smoke/integration-heavy; run `./test.sh all` before large changes.
- Add deterministic tests near related code under `tests/` or as root-level `test_*.py`.

## Commit & Pull Request Guidelines
- Follow Conventional Commits: `feat`, `fix`, `docs`, `chore`, optionally scoped (for example, `feat(search): ...`).
- Keep commits focused, and link issues when applicable (`fixes #123`).
- Use `.github/PULL_REQUEST_TEMPLATE.md`: include change type, summary, test steps, and linked issue.
- Include screenshots for UI changes (`apps/dsa-web` or WebUI), and update docs for config/behavior changes.

## Security & Configuration Tips
- Never commit `.env`, API keys, webhook tokens, or private credentials.
- Add new environment variables to `.env.example` and document them in `README.md` or `docs/`.
