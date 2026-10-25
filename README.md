# DeploySmith OS Frontend

Static deploy UI for DeploySmith OS. Deploys to GitHub Pages on every push to `main`.

## Structure

- `index.html`, `app.js`, `style.css` — static deploy UI (deploy form, SSE event stream, apps list)
- `src/`, `public/`, `vite.config.ts` — original React/Vite app (kept for reference)
- `.github/workflows/frontend-deploy.yml` — GitHub Actions → GitHub Pages deploy

## Connection to backend

`app.js` calls the backend API at `http://localhost:8000` by default (set via the `data-api-base` attribute on the `<script>` tag). When deploying the backend to a host, update that value to your backend URL (e.g. `https://your-backend.example.com`).

The frontend expects these backend endpoints:
- `GET /api/health`
- `POST /api/deployments` (header `X-DeploySmith: 1`, body `{ "repo_url": "..." }`)
- `GET /api/deployments/{id}/events` (SSE)
- `GET /api/apps`

## Deploy

Push to `main`. GitHub Pages is configured via the `frontend-deploy.yml` workflow. Enable Pages in repo settings (Source: GitHub Actions).
