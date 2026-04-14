# Dockerized setup with Neon Local (development) and Neon Cloud (production)

This project is configured to run in two modes:

- Development: app + Neon Local proxy in Docker (`docker-compose.dev.yml`)
- Production: app only in Docker, connected directly to Neon Cloud (`docker-compose.prod.yml`)

## Files added

- `Dockerfile`
- `docker-compose.dev.yml`
- `docker-compose.prod.yml`
- `docker-compose.yml` (default development compose)
- `.env.development`
- `.env.production`

## How environment switching works

Your app always reads `DATABASE_URL` from environment variables:

- Development (`.env.development`): `DATABASE_URL=postgres://neon:npg@neon-local:5432/neondb`
- Production (`.env.production`): `DATABASE_URL=postgres://...neon.tech...`

`src/config/database.js` now auto-detects Neon Local hosts (`neon-local`, `localhost`, `127.0.0.1`) and configures the Neon serverless driver to use the local SQL endpoint (`/sql`) automatically.

## Development (local) with Neon Local

1. Update `.env.development`:
   - `NEON_API_KEY`
   - `NEON_PROJECT_ID`
2. Start services:
   - `docker compose -f docker-compose.dev.yml --env-file .env.development up --build`
   - or `docker compose --env-file .env.development up --build` (uses `docker-compose.yml`)
3. App is available on:
   - `http://localhost:3000`

In development, the app connects through Neon Local at:

- `postgres://neon:npg@neon-local:5432/neondb`

Neon Local creates ephemeral branches by default when the container starts and removes them when the container stops (`DELETE_BRANCH=true`).

## Production with Neon Cloud

1. Update `.env.production`:
   - `DATABASE_URL=postgres://...neon.tech...`
2. Start production app:
   - `docker compose -f docker-compose.prod.yml --env-file .env.production up --build -d`

Production runs without Neon Local proxy and connects directly to Neon Cloud.

## Notes

- Keep production secrets in deployment environment variables (CI/CD secrets, cloud secrets manager, etc.).
- Do not hardcode `DATABASE_URL` in code.
