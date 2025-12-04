# Repository Guidelines

## Project Structure & Modules
- `client/`: React Router 7 front end (TypeScript). Key folders: `app/routes` for pages, `app/components` for UI and blocks, `app/lib` for utilities, `app/types` for shared types.
- `server/`: Strapi 5 backend. `src/api` holds content-type APIs, `src/components` for Strapi components, `config/` for environment/config overrides.
- Root scripts orchestrate both apps; seed data lives in `seed-data.tar.gz`. Environment copies are handled via `copy-env.mts`.

## Build, Test, and Development Commands
- Install & setup everything: `yarn setup` (runs client/server installs and copies env files).
- Run both dev servers: `yarn dev` (client on 5173, Strapi on 1337 after wait-on).
- Seed Strapi data: `yarn seed`; export current data: `yarn export`.
- Client only: `cd client && yarn dev` (dev), `yarn build` (production build), `yarn start` (serve build), `yarn typecheck` (type generation + `tsc`).
- Server only: `cd server && yarn develop` (admin + APIs), `yarn build` (admin build), `yarn start` (serve built app).

## Coding Style & Naming
- Language: TypeScript across client and server; prefer typed helpers in `app/lib` and shared `app/types`.
- React: functional components; co-locate route loaders/actions with route files in `app/routes`.
- Naming: kebab-case for routes, PascalCase for components, camelCase for functions/vars. Keep Strapi APIs under clear folders (`src/api/<content-type>`).
- Formatting: follow existing patterns; run `yarn typecheck` in `client` before committing. Use consistent imports and avoid default exports unless required by framework.

## Testing Guidelines
- No automated test suite is present; rely on type checks plus manual flows (auth, article CRUD, image rendering).
- Add unit or integration tests when introducing risky logic; prefer colocated tests near modules. Name test files `*.test.ts[x]`.
- For Strapi changes, validate content-type changes via admin UI and re-run `yarn seed` if schema updates require fixtures.

## Commit & Pull Request Guidelines
- Recent history uses short imperative messages (e.g., “cleanup and prepare content types”); keep messages concise and action-oriented.
- Branch naming: `feature/<topic>` or `fix/<topic>` is preferred for clarity.
- PRs: include summary of scope, linked issue (if any), screenshots for UI changes, and notes on data/model migrations. Mention any new env vars or scripts.

## Environment & Security Notes
- Node 18–22 supported; use Yarn 1.x (matching `.yarnrc`/lock). Ensure `.env` exists in both `client` and `server` (copied from provided examples).
- Avoid committing `.env`, `seed-data.tar.gz`, or build artifacts. Regenerate seeds with `yarn export` before sharing schema/data changes.
