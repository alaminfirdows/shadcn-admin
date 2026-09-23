# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Read first

`project-context.md` (repo root) is the source of truth for scope, decisions, and phasing — read it before starting any non-trivial task. `AGENTS.md` also applies: this is Next.js 16, not the Next.js in your training data — check `node_modules/next/dist/docs/` (app router: `01-app/`, pages router: `02-pages/`) before writing routing/data-fetching/config code, and heed deprecation notices.

## What this repo is

A public **shadcn/ui showcase + installable registry** (`shadcn-showcase`), not a single dashboard template. Every page/block demonstrates a reusable, composable UI pattern that can be copied or installed via `npx shadcn add <name>` (self-hosted registry, no npm package). Currently a fresh Next.js starter — the ~300+ page showcase (component gallery, blocks library, flagship CRM/E-commerce suites, then other dashboard/app families) is built out in phases per `project-context.md`. No backend/auth/database: all data comes from deterministic mock fixtures.

## Commands

- `pnpm dev` — start dev server
- `pnpm build` / `pnpm start` — production build / serve
- `pnpm lint` — ESLint (see "Known issue" below — currently broken repo-wide)
- `pnpm typecheck` — `tsc --noEmit`, strict mode
- `pnpm format` — Prettier write, `**/*.{ts,tsx}`
- No test script/framework is configured yet.

Package manager is **pnpm** (`pnpm-lock.yaml`, `pnpm-workspace.yaml`) — don't use npm/yarn.

### Known issue: `pnpm lint` currently crashes

`eslint-plugin-react` (pulled in via `eslint-config-next`) is incompatible with ESLint 10 (`contextOrFilename.getFilename is not a function`, in `react/display-name`). This must be fixed before `@shadcn/lint` can gate anything — it's phase-0 work in `project-context.md`. Don't assume a clean `pnpm lint` run means your code is clean until this is resolved.

## Architecture

**Stack**: Next.js 16 (App Router), React 19, TypeScript strict, Tailwind v4, shadcn/ui.

**shadcn setup** (`components.json`): style `base-vega`, base color `neutral`, icon library `lucide`, RSC on, no Tailwind prefix. Path aliases (also in `tsconfig.json` as `@/*` → repo root):
- `@/components` → `components/`
- `@/components/ui` → `components/ui/` (shadcn primitives — add via `npx shadcn add`, don't hand-roll)
- `@/lib` → `lib/`, `@/lib/utils` → `cn()` helper
- `@/hooks` → `hooks/`

**Target repo structure** (being built out per `project-context.md`'s phased plan — not all present yet):
```
app/(site)/            marketing/docs shell for the showcase itself
app/components/        component showcase pages
app/blocks/            block gallery pages
app/dashboards/<family>/  CRM, E-commerce, SaaS, Finance, HR, PM, Support, ...
app/applications/      Mail, Chat, Calendar, Notes, Files, Notifications
app/r/[name]/route.ts  registry.json server (self-hosted registry)
components/{navigation,data-display,forms,charts,commerce,crm,shared}/
blocks/<family>/       registry-installable compositions
lib/mock/              shared, deterministic domain data generators — build once
                       per domain (customers, deals, products, ...), never per page
registry/              registry.json item definitions
content/                per-block/page docs (MDX)
```
CRM and E-commerce are the flagship suites (built first, full state variants: empty/loading/error/permission); other dashboard families follow the same block → page pattern afterward.

**Token discipline**: `@shadcn/lint` (wired into `eslint.config.mjs`) enforces `no-restyle`, `no-raw-colors`, `no-arbitrary-values`, `no-inline-styles`, `no-unknown-classes`, `require-static-classes`. Style with design tokens/Tailwind utilities and `cn()`/`cva()` variants, not raw colors or arbitrary values, once lint is unblocked.

**Formatting**: Prettier, no semicolons, double quotes, 2-space tabs, 80 print width, `prettier-plugin-tailwindcss` (auto-sorts Tailwind classes, stylesheet `app/globals.css`, functions `cn`/`cva`).

## Subagents

`.claude/agents/coder.md` (feature/bug implementation) and `.claude/agents/fixer.md` (lint/typecheck/format-only fixes, no `eslint-disable`/`@ts-ignore`/`any` suppressions without justification) are configured for this repo — prefer them for their respective scopes.
