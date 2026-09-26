# Contributing

Some of this is proposed rather than settled. Items marked **proposed** are open for the owner to change.

## Setup

Follow the README. Use pnpm 10. The root `preinstall` script rejects npm and yarn.

## Branches and commits (proposed)

- Branch from `main`. Name branches `feat/...`, `fix/...`, `chore/...`, `docs/...`.
- Open pull requests against `main` from a fork or feature branch.
- Use [Conventional Commits](https://www.conventionalcommits.org/) for commit subjects, for example `feat(api): add token balance route`.
- Rebase on `main` before opening or updating a PR.

## Before you push

```sh
pnpm run typecheck
pnpm --filter @workspace/api-server run build
```

CI runs the same checks on every pull request.

## Rules that are already enforced by the repo

- pnpm only. Do not add `package-lock.json` or `yarn.lock`.
- Do not lower or remove `minimumReleaseAge` in `pnpm-workspace.yaml`. Add exceptions to `minimumReleaseAgeExclude` only for trusted publishers, and remove them once the release is a day old.
- Shared dependency versions live in the `catalog:` section of `pnpm-workspace.yaml`. Reference them with `"catalog:"` in a package's `package.json`.
- Never edit files under `lib/*/src/generated/`. Change `lib/api-spec/openapi.yaml` and run codegen instead.
- Never commit `.env`.

## Adding an API endpoint

1. Add the path and schemas to `lib/api-spec/openapi.yaml`.
2. `pnpm --filter @workspace/api-spec run codegen`
3. Create or extend a router under `artifacts/api-server/src/routes/` and mount it in `routes/index.ts`.
4. Validate the response with the generated schema from `@workspace/api-zod` before sending it.

## Adding a database table

1. Create `lib/db/src/schema/<table>.ts` following the template in `schema/index.ts`.
2. Export it from `schema/index.ts`.
3. `DATABASE_URL=... pnpm --filter @workspace/db run push`

## Tests (proposed)

No test runner is configured yet. The proposal is Vitest with tests next to the code as `*.test.ts`. This will be added once the owner confirms.

## Questions

Open questions for the project owner are tracked in [docs/CONTRIBUTING-QUESTIONS.md](docs/CONTRIBUTING-QUESTIONS.md).
