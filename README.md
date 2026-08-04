# my-monrepo

A [Turborepo](https://turborepo.dev/) monorepo containing two Next.js applications and their shared packages.

## What's inside

### Apps

| App    | Description                    | Dev port |
| ------ | ------------------------------- | -------- |
| `web`  | Main Next.js application        | 3000     |
| `docs` | Next.js documentation site      | 3001     |

### Packages

| Package                  | Description                                              |
| ------------------------ | ---------------------------------------------------------- |
| `@repo/ui`               | Shared React component library used by `web` and `docs`  |
| `@myapp/utils`           | Shared utility functions (e.g. `formatDate`, `slugify`)  |
| `@repo/eslint-config`    | Shared ESLint configs (base, Next.js, React internal)    |
| `@repo/typescript-config`| Shared `tsconfig.json` bases                              |

Everything is written in [TypeScript](https://www.typescriptlang.org/).

## Tech stack

- [Next.js 16](https://nextjs.org/) + [React 19](https://react.dev/)
- [Turborepo](https://turborepo.dev/) for task orchestration and caching
- [pnpm](https://pnpm.io/) workspaces for package management
- [ESLint 9](https://eslint.org/) + [Prettier](https://prettier.io/)

## Prerequisites

- Node.js 20.9 or later (required by Next.js 16)
- [pnpm](https://pnpm.io/installation) 9 (`corepack enable` will pick up the version pinned in `package.json`)

## Getting started

Install dependencies from the repo root:

```sh
pnpm install
```

Run every app in dev mode:

```sh
pnpm dev
```

`web` starts on [localhost:3000](http://localhost:3000) and `docs` on [localhost:3001](http://localhost:3001).

Run a single app with a [Turborepo filter](https://turborepo.dev/docs/crafting-your-repository/running-tasks#using-filters):

```sh
pnpm turbo dev --filter=web
pnpm turbo dev --filter=docs
```

## Available scripts

Run from the repo root, these fan out to every app/package via Turborepo:

```sh
pnpm build         # Build all apps and packages
pnpm dev           # Run all apps in dev mode
pnpm lint          # Lint all apps and packages
pnpm check-types   # Type-check all apps and packages
pnpm format        # Format the repo with Prettier
```

Scope any of these to one app with `--filter`, e.g. `pnpm turbo build --filter=docs`.

## Project structure

```
apps/
  web/     # Main Next.js app
  docs/    # Docs Next.js app
packages/
  ui/                 # Shared React components (@repo/ui)
  utils/              # Shared utilities (@myapp/utils)
  eslint-config/      # Shared ESLint configs (@repo/eslint-config)
  typescript-config/  # Shared tsconfig bases (@repo/typescript-config)
```

## Remote caching

Turborepo caches task output locally by default. To share the cache across your team and CI, connect to [Vercel Remote Cache](https://turborepo.dev/docs/core-concepts/remote-caching) (or a self-hosted alternative):

```sh
pnpm turbo login
pnpm turbo link
```
