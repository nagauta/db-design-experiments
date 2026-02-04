# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build and Development Commands

```bash
# Install dependencies
pnpm install

# Development (all apps)
pnpm run dev

# Development (specific app)
pnpm run dev --filter=web
pnpm run dev --filter=docs

# Build all apps and packages
pnpm run build

# Build specific app
pnpm run build --filter=web

# Lint all packages
pnpm run lint

# Type check
pnpm run check-types

# Format code
pnpm run format
```

## Architecture

This is a Turborepo monorepo using pnpm workspaces.

### Workspace Structure

- `apps/web` - Next.js application (port 3000)
- `apps/docs` - Next.js documentation app
- `packages/ui` - Shared React component library (`@repo/ui`)
- `packages/eslint-config` - Shared ESLint configuration (`@repo/eslint-config`)
- `packages/typescript-config` - Shared TypeScript configuration (`@repo/typescript-config`)

### Package Dependencies

Apps import shared packages using workspace protocol:
- `@repo/ui` - Import components via `@repo/ui/ComponentName`
- `@repo/eslint-config` - ESLint configurations
- `@repo/typescript-config` - TypeScript base configs

### Turborepo Task Configuration

Tasks defined in `turbo.json`:
- `build` - Builds with dependency order (`^build`), outputs `.next/**`
- `dev` - Persistent dev server, no caching
- `lint` - Linting with dependency order
- `check-types` - TypeScript type checking

## Commit Convention

This project follows [Conventional Commits](https://www.conventionalcommits.org/).

Format: `<type>(<scope>): <description>`

Types:
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation only
- `style` - Code style (formatting, semicolons, etc.)
- `refactor` - Code refactoring (no feature/fix)
- `perf` - Performance improvement
- `test` - Adding/updating tests
- `chore` - Build process, tooling, dependencies

Scope (optional): `web`, `docs`, `ui`, `eslint-config`, `typescript-config`

Examples:
```
feat(web): add user authentication
fix(ui): correct button hover state
chore: update dependencies
```
