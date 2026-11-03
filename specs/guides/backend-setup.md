# Backend setup

The FastAPI service handles document processing, retrieval, AI orchestration, analyses, and report drafting. You need Python 3.12+, `uv`, a Supabase project, and OpenAI and Anthropic API keys.

## Configure and start

1. Copy `backend/.env.example` to `backend/.env` and fill in the Supabase URL and keys, database URLs, and model API keys. Use the direct database URL for migrations. See the [Supabase setup guide](supabase-setup.md) for where to find these values.
2. From `backend/`, install dependencies, apply migrations, and start the API:

```powershell
uv sync
uv run alembic upgrade head
uv run python run.py
```

The API listens on `http://127.0.0.1:8000`; `GET /health` returns a health response. `run.py` selects a compatible event loop on Windows.

`backend/app/config.py` defines the required environment variables. Keep the Supabase service key and model API keys in the backend environment only.
