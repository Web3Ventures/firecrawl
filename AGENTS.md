# Repository Guidelines

## Project Structure & Module Organization
Firecrawl is a monorepo under `apps/`:
- `apps/api` is the main API + workers (TypeScript/Node).
- `apps/ui/ingestion-ui` is the web UI.
- SDKs live in `apps/js-sdk`, `apps/python-sdk`, and `apps/rust-sdk`.
- Supporting services include `apps/playwright-service-ts`, `apps/go-html-to-md-service`, and `apps/redis`.
- Database tooling is in `apps/nuq-postgres` (includes `nuq.sql`).
Examples and demos are in `examples/`, and assets are in `img/`.

## Build, Test, and Development Commands
- `cd apps/api && pnpm install` installs API dependencies (pnpm 9+).
- `redis-server` starts Redis locally (required by the API).
- `cd apps/api && pnpm start` builds and runs the API harness/workers.
- `cd apps/api && pnpm dev` runs the harness in dev mode.
- `curl -X GET http://localhost:3002/test` checks the local API.
- `docker compose up` from the repo root runs Redis + API + workers via Docker.

## Coding Style & Naming Conventions
- TypeScript/JavaScript in `apps/api` is formatted with Prettier (2-space indent, semicolons, LF).
- UI code in `apps/ui/ingestion-ui` uses ESLint; follow existing patterns there.
- Rust uses `rustfmt` (`apps/api/native`), and Go services use `gofmt`.
- Tests typically follow `*.test.ts` naming under `apps/api/src/__tests__/`.

## Testing Guidelines
- API tests use Jest: `cd apps/api && pnpm test` or the faster subset `pnpm test:snips`.
- The broader system suite lives in `apps/test-suite` and runs with Playwright:
  `cd apps/test-suite && npm install && npx playwright install && npm run test`.
- Load testing (optional): `cd apps/test-suite && artillery run load-test.yml`.

## Commit & Pull Request Guidelines
- Use short, imperative commit summaries. Conventional commits with scope are common
  (e.g., `feat(api): add map headers`), and issue/PR numbers are often appended.
- PRs should include: a clear description, steps to test, and screenshots for UI changes.
- Update docs or examples when behavior or endpoints change.

## Security & Configuration Tips
- Copy `apps/api/.env.example` to `apps/api/.env` and set required env vars.
- Local Postgres is expected; you can build the Docker image in `apps/nuq-postgres`
  or run the SQL in `apps/nuq-postgres/nuq.sql`.
