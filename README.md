# earthtoken-accounting-gamification

> Product description pending owner input. See [docs/CONTRIBUTING-QUESTIONS.md](docs/CONTRIBUTING-QUESTIONS.md).

Repository tagline: *realtime, acting locally, reword search, evidence based, vetted earth information.*

## Stack

- pnpm 10 workspaces, Node.js 24, TypeScript 5.9
- API: Express 5, pino logging, bundled with esbuild
- Database: PostgreSQL via Drizzle ORM
- Validation: Zod v4, drizzle-zod
- API codegen: Orval, from `lib/api-spec/openapi.yaml`
- UI preview: Vite 7, React 19, Tailwind 4, shadcn/ui

## Workspace layout

| Package | Path | Purpose |
|---|---|---|
| `@workspace/api-server` | `artifacts/api-server` | Express API. Routes under `src/routes/` |
| `@workspace/mockup-sandbox` | `artifacts/mockup-sandbox` | Replit canvas component preview server. Not a product frontend |
| `@workspace/api-spec` | `lib/api-spec` | OpenAPI contract (source of truth) and Orval config |
| `@workspace/api-zod` | `lib/api-zod` | Generated Zod schemas. Do not edit by hand |
| `@workspace/api-client-react` | `lib/api-client-react` | Generated react-query hooks plus `custom-fetch.ts` |
| `@workspace/db` | `lib/db` | Drizzle client and schema (`src/schema/`) |
| `@workspace/scripts` | `scripts` | One-off scripts run with tsx |

## Prerequisites

- Node.js 24
- pnpm 10.x (the lockfile is v9; pnpm 11 rewrites `pnpm-workspace.yaml` on install)
- PostgreSQL 15+ reachable via `DATABASE_URL`

## Run locally

```sh
cp .env.example .env          # then edit DATABASE_URL
pnpm install --frozen-lockfile
pnpm run typecheck
DATABASE_URL=... pnpm --filter @workspace/db run push
PORT=5050 pnpm --filter @workspace/api-server run dev
curl http://localhost:5050/api/healthz
```

Environment variables are not auto-loaded. Export them in your shell or prefix the command.

| Variable | Used by | Notes |
|---|---|---|
| `DATABASE_URL` | `lib/db`, drizzle-kit | Postgres connection string |
| `PORT` | api-server, mockup-sandbox | Required, no default |
| `BASE_PATH` | mockup-sandbox | Replit sets `/__mockup` |
| `LOG_LEVEL` | api-server | Optional, defaults to `info` |

## Common commands

```sh
pnpm run typecheck                              # every package
pnpm run build                                  # typecheck then build
pnpm --filter @workspace/api-spec run codegen   # after editing openapi.yaml
pnpm --filter @workspace/db run push            # sync schema to the dev database
```

## API workflow

1. Edit `lib/api-spec/openapi.yaml`. Keep `info.title` as `Api`; every operation needs an `operationId` and a tag.
2. Run codegen. It regenerates `lib/api-zod` and `lib/api-client-react`, then typechecks the libs.
3. Add a router file under `artifacts/api-server/src/routes/` and mount it in `routes/index.ts`. Parse responses through the generated Zod schema, as `routes/health.ts` does.

## Database workflow

One table per file under `lib/db/src/schema/`, re-exported from `schema/index.ts`. Each file defines the Drizzle table, an insert schema via `createInsertSchema`, and the inferred types. The template is in the comment at the top of `schema/index.ts`.

## macOS note

`pnpm-workspace.yaml` removes non-Linux native binaries to keep Replit images small. On macOS, esbuild recovers on its own during install, so the API server builds and runs. The mockup sandbox does not start on macOS because Rollup's darwin binary is excluded. Port 5000 is also claimed by AirPlay Receiver on recent macOS, so use another port.

## Deployment

Configured for Replit autoscale via `.replit` and `artifacts/*/.replit-artifact/artifact.toml`. Production runs `node artifacts/api-server/dist/index.mjs` on port 8080 with `/api/healthz` as the startup health check. `scripts/post-merge.sh` runs install and schema push after merges.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).
