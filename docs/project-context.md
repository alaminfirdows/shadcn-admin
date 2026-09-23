# Project Context — shadcn-showcase

## What this is

A public **shadcn/ui showcase + installable registry**, not a single dashboard
template. Every example demonstrates a reusable UI pattern (real composition,
realistic mock data, responsive behavior, loading/empty/error states) that can
be copied or installed via the shadcn CLI — in line with shadcn's open-code,
composable-blocks philosophy rather than a closed component package.

Four layers, each buildable and browsable on its own:

```
Design Tokens → Primitives (shadcn ui/) → Components → Blocks → Pages/Apps
```

## Decisions (locked in during scoping)

| Question | Decision |
|---|---|
| Repo location | Extend this repo (`shadcn-admin` → `shadcn-showcase`), keep existing base-vega style, aliases, and the Button component already installed |
| Primary goal | Public showcase site **and** a real shadcn registry (`npx shadcn add <name>` works) |
| Phase 1 scope | Full scope (~300+ pages) as the north star, delivered in phases — flagships first |
| Data source | Static mock fixtures (deterministic, faker-generated), no backend, no auth |
| Registry | Built from day one — every block/page is a `registry.json` item |
| State variants (empty/loading/error/permission) | Flagship-only first (CRM + E-commerce), then expand to other families |
| Token strictness | Enforced now via `@shadcn/lint` (`no-restyle`, `no-raw-colors`, `no-arbitrary-values`, `no-inline-styles`, `no-unknown-classes`, `require-static-classes`) |
| Component base | Reuse existing shadcn setup already in this repo (no re-init) |
| Project name | `shadcn-showcase` |
| Themes | Light/dark + 4 token themes: default/neutral, blue, green, rose |
| Deployment | Vercel |

## Non-goals (for now)

- No live backend, database, or auth — pages are static demos over mock data.
- No i18n system. RTL appears only as one nav-gallery example.
- No export-to-other-builders engine (Elementor/Bricks/Gutenberg) — token
  discipline is enforced so that door stays open later, but nothing is built
  toward it yet.
- No npm-published package — the registry is self-hosted from this app's own
  routes (`/r/[name].json`), same pattern as the official shadcn docs site.

## Starting state (as of repo inspection)

Fresh Next.js starter: `app/layout.tsx`, `app/page.tsx` (placeholder "Project
ready!" page), `app/globals.css`, one component (`components/ui/button.tsx`),
`components/theme-provider.tsx`, `lib/utils.ts`. Nothing to migrate — the
showcase is additive from here.

## Repository structure (target)

```
shadcn-showcase/
├── app/
│   ├── (site)/                 # marketing/docs shell for the showcase itself
│   ├── components/             # component showcase pages
│   ├── blocks/                 # block gallery pages
│   ├── dashboards/<family>/    # CRM, E-commerce, SaaS, Finance, HR, PM,
│   │                           # Support, Healthcare, Real Estate, Logistics, Crypto
│   ├── applications/           # Mail, Chat, Calendar, Notes, Files, Notifications
│   ├── authentication/
│   ├── settings/
│   ├── marketing/
│   ├── states/                 # empty/loading/error/permission galleries
│   └── r/[name]/route.ts       # registry.json server
│
├── components/
│   ├── ui/                     # shadcn primitives
│   ├── navigation/ data-display/ forms/ charts/ commerce/ crm/ shared/
│
├── blocks/
│   ├── crm/  ecommerce/  saas/ ...   # registry-installable compositions
│
├── lib/
│   └── mock/                   # shared, deterministic domain data generators
│       (customers, deals, products, orders, employees, tickets, ...)
│
├── registry/                   # registry.json item definitions
└── content/                    # per-block/page docs (MDX)
```

## Scope reference (target page counts)

| Category | Target |
|---|---|
| UI components | 50+ |
| Component compositions | 100+ |
| Navigation patterns (sidebar/header) | 26 |
| Table patterns | 15 |
| Form patterns | 20 |
| Chart examples | 25+ |
| Marketing sections | 50+ |
| Auth pages | 15+ |
| CRM pages | 20 |
| E-commerce pages | 20 |
| SaaS / Finance / HR / Project Management / Support | 10 each |
| Healthcare / Real Estate / Logistics / Crypto | 8 each |
| Application pages (Mail, Chat, Calendar, Notes, Files, Notifications) | 20+ |
| Settings pages | 17 |
| Empty / loading / error / permission states | 30+ (flagships first) |

CRM and E-commerce are the **flagship suites**: each of their 20 pages is a
deliberately distinct information architecture (overview, pipeline/kanban,
detail views, analytics, command-center), not a reskin of the same layout —
see the phased plan for the full page-by-page breakdown of both.

## Build sequencing (phases)

0. Foundation — folder structure, mock-data layer, registry tooling,
   `@shadcn/lint` enforcement (fix the pre-existing ESLint 10 /
   `eslint-plugin-react` crash first), theme tokens, site shell/nav.
1. Component showcase — full shadcn primitive set + real-world compositions.
2. Blocks library — CRM and E-commerce blocks, shared dashboard layout shells.
3. Flagship suites — CRM-01…20, ECOM-01…20, state variants, responsive +
   theme verification (flagships only).
4. Remaining dashboard families (SaaS, Finance, HR, PM, Support, Healthcare,
   Real Estate, Logistics, Crypto) via the same block→page pattern.
5. Cross-cutting galleries — auth, settings, profiles, data tables, forms,
   charts, modals/drawers, generic apps, marketing, general states.
6. Registry finalization, docs, CI, Vercel deploy, public launch.

## Known risks

- `pnpm lint` is currently broken repo-wide (`eslint-plugin-react` vs
  ESLint 10 incompatibility) — must be fixed before `@shadcn/lint` can
  actually gate anything.
- 300+ pages is a multi-month effort; each phase above is a real milestone,
  not a single pass.
- Registry-from-day-one adds per-block schema/dependency overhead that will
  slow early velocity in exchange for a working `npx shadcn add` experience.
- Static fixtures risk drifting/duplicating across 300+ pages unless the
  `lib/mock/` domain layer is shared consistently — build it once per domain,
  not per page.
- "shadcn-showcase" as a public name hasn't been checked for collisions.
