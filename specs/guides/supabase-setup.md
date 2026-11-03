# Supabase setup

Dossier uses Supabase for Postgres and email authentication. Create a Supabase project, then configure the backend and frontend using their environment templates:

- `backend/.env.example` → `backend/.env` (server credentials)
- `frontend/.env.example` → `frontend/.env` (browser-safe values only)

## Values to collect

| Value | Supabase dashboard | Environment variable |
| --- | --- | --- |
| Project URL | Project Settings → API | `SUPABASE_URL` / `VITE_SUPABASE_URL` |
| Publishable key | Project Settings → API Keys | `SUPABASE_PUBLISHABLE_KEY` / `VITE_SUPABASE_ANON_KEY` |
| Service key | Project Settings → API Keys | `SUPABASE_SERVICE_KEY` (backend only) |
| Pooled database URL | Project Settings → Database → Connection strings | `DATABASE_URL` |
| Direct database URL | Project Settings → Database → Connection strings | `DATABASE_URL_DIRECT` |

Keep the service key, database URLs, and model API keys out of the frontend environment and version control. The frontend only needs the publishable key.

## Authentication and migrations

Enable email sign-in under Authentication → Sign-in providers. For local development, configure email confirmation according to your test setup.

From `backend/`, apply the checked-in Alembic migrations with:

```powershell
uv run alembic upgrade head
```

Use the direct database URL for migrations. Review schema changes before applying them to any shared or production database.
