# Frontend setup

The frontend is a React and Vite app. You need Node.js and pnpm.

## Configure and run

Copy `frontend/.env.example` to `frontend/.env` and set the API URL, Supabase project URL, and publishable key. These values are used by the browser app; do not put server secrets in this file.

From `frontend/`:

```powershell
pnpm install
pnpm dev
```

Vite prints the local development URL after startup. The frontend expects the FastAPI service to be running at the URL configured by `VITE_API_BASE_URL`.
