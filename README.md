# Emapta

## Quick test: full stack (Docker)

From **this directory** (where `docker-compose.yml` lives):

1. Install [Docker Desktop](https://docs.docker.com/desktop/) (or any Docker engine with Compose v2).
2. Start Postgres, API, and UI:

   ```bash
   docker compose up
   ```

   Rebuild images after Dockerfile or lockfile changes:

   ```bash
   docker compose up --build
   ```

3. Open in the browser:

   - **UI:** [http://localhost:5174](http://localhost:5174) (host **5174** → Vite **5173** in the container, so it does not collide with a local Vite on 5173).
   - **API health:** [http://localhost:3000/health](http://localhost:3000/health)
   - **Swagger:** [http://localhost:3000/api-docs](http://localhost:3000/api-docs)

If the database gets into a bad state (for example duplicate migration errors), reset the volume and start again:

```bash
docker compose down -v
docker compose up
```

**Note:** Compose publishes Postgres on host port **5432**. If something else already uses that port, change the mapping in `docker-compose.yml` or stop the conflicting service.

---

## Test only `project-simulator` (API)

### With Docker (same compose)

The API is the **`backend`** service. After `docker compose up`, use the URLs above on port **3000** — no extra steps.

## Layout

| Path | Role |
|------|------|
| `docker-compose.yml` | Postgres + backend + frontend for local integration testing. |
| `project-simulator/` | Backend source, `Dockerfile`, `.env.example`, Jest tests. |
| `project-simulator-front/` | Frontend source and `Dockerfile`. |

For more backend-only detail, see `project-simulator/README.md`.
