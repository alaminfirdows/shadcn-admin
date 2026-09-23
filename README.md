# shadcn-showcase

A public **shadcn/ui showcase + installable registry**, not a single dashboard template. Every example demonstrates a reusable UI pattern (real composition, realistic mock data, responsive behavior, loading/empty/error states) that can be copied or installed via `npx shadcn add <name>` — in line with shadcn's open-code, composable-blocks philosophy.

**~300+ pages** across design system, components, blocks, dashboard families, and applications. Full scope delivered in phases — flagships (CRM + E-commerce) first.

## Quick start

```bash
# Install dependencies
pnpm install

# Start dev server
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) to browse the showcase.

## Commands

- `pnpm dev` — Start dev server
- `pnpm build` — Production build
- `pnpm start` — Serve production build
- `pnpm lint` — ESLint (currently blocked by eslint-plugin-react incompatibility with ESLint 10)
- `pnpm typecheck` — TypeScript strict check
- `pnpm format` — Prettier write

## Architecture

**Stack**: Next.js 16 (App Router), React 19, TypeScript strict, Tailwind v4, shadcn/ui.

**Four layers** (each browsable and installable on its own):
```
Design Tokens → Primitives (shadcn ui/) → Components → Blocks → Pages/Apps
```

**Directory structure** (target, built in phases):
```
app/(site)/              Marketing/docs shell
app/components/          Component showcase pages
app/blocks/              Block gallery pages
app/dashboards/<family>/ CRM, E-commerce, SaaS, Finance, HR, PM, Support, ...
app/applications/        Mail, Chat, Calendar, Notes, Files, Notifications
app/r/[name]/route.ts    Registry.json server (self-hosted)

components/ui/           shadcn primitives
components/{navigation,data-display,forms,charts,commerce,crm,shared}/
blocks/<family>/         Registry-installable compositions
lib/mock/                Shared, deterministic domain data generators
```

## Development

**Setup**: shadcn is already initialized with `base-vega` style, neutral color base, lucide icons. Path aliases configured: `@/components`, `@/components/ui`, `@/lib`, `@/lib/utils` (cn helper).

**Adding UI components**: Use shadcn CLI:
```bash
npx shadcn@latest add button
```
Components land in `components/ui/`.

**Token discipline**: `@shadcn/lint` enforces design-token usage only (no restyle, raw colors, arbitrary values, inline styles, unknown classes).

## Build phases

0. **Foundation** — Folder structure, mock-data layer, registry tooling, lint enforcement, theme tokens, site shell/nav
1. **Component showcase** — Full shadcn primitive set + real-world compositions
2. **Blocks library** — CRM and E-commerce blocks, shared dashboard layout shells
3. **Flagship suites** — CRM (20 pages) & E-commerce (20 pages), state variants (empty/loading/error/permission), responsive + theme verification
4. **Remaining dashboard families** — SaaS, Finance, HR, PM, Support, Healthcare, Real Estate, Logistics, Crypto
5. **Cross-cutting galleries** — Auth, settings, profiles, data tables, forms, charts, modals, generic apps, marketing
6. **Registry finalization, docs, CI, Vercel deploy**

## Themes

Light/dark mode + 4 token themes: default/neutral, blue, green, rose.

## Registry

Every block and page is a registry item (installable via `npx shadcn add`). Self-hosted from `app/r/[name]/route.ts` — same pattern as official shadcn docs.

## Data

Static mock fixtures (deterministic, faker-generated). No backend, database, or auth. Domain data generators in `lib/mock/` are built once per domain (customers, deals, products, orders, etc.) and shared across pages.

## Known issues

- `pnpm lint` currently crashes due to `eslint-plugin-react` incompatibility with ESLint 10. Must be fixed before lint gates anything (phase-0 work).

## Learn more

See `project-context.md` for full scope, decisions, known risks, and detailed phasing breakdown.
