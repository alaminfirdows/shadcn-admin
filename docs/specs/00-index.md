# Specs Index

Detailed, implementation-ready specs for every component, block, and page in
`shadcn-showcase`, per `project-context.md`. These are **specs only** —
nothing here is implemented yet. Each file below is scoped so it can be
handed off and built independently once you say go.

## Files

| File | Covers | Phase(s) |
|---|---|---|
| `01-components-navigation.md` | Full shadcn primitive showcase (50+) + sidebar (15) + header (11) patterns | 1 |
| `02-blocks.md` | Registry-installable blocks: CRM (8), E-commerce (6), dashboard layout shells (5) | 2 |
| `03-dashboards-crm.md` | CRM-01…20 flagship suite | 3 |
| `04-dashboards-ecommerce.md` | ECOM-01…20 flagship suite | 3 |
| `05-dashboards-other-families.md` | SaaS(10) Finance(10) HR(10) PM(10) Support(10) Healthcare(8) Real Estate(8) Logistics(8) Crypto(8) — 82 pages | 4 |
| `06-applications.md` | Mail, Chat, Calendar, Notes, Files, Notifications | 5 |
| `07-authentication-settings-profile.md` | Auth (15+), Settings (17 sections), Profile (3 variants) | 5 |
| `08-data-tables-forms-charts.md` | Table gallery (15), Form gallery (11 layouts + 13 forms), Chart gallery (19+) | 5 |
| `09-states-modals.md` | Generic empty/loading/error/permission gallery, flagship state matrix, Modal/Drawer gallery (13) | 3 & 5 |
| `10-marketing.md` | Landing pages (3), marketing section library, Bento gallery | 5 |

## Conventions used in every file

**Entry template:**
```
### <ID> — <Name>
- Route: `/...`
- Purpose: one line
- Sections (top → bottom): ordered list of what's on the page
- Blocks used: registry block names from 02-blocks.md, where applicable
- Components: shadcn primitives involved
- Data entities: which `lib/mock/<entity>.ts` generator(s) it reads
- States: which of [E]mpty [L]oading [Er]ror [P]ermission [F]iltered [Sel]ected apply, and in which phase they ship
- Phase: build phase from project-context.md
```

**Routes** are kebab-case, grouped by area: `/dashboards/<family>/<page>`,
`/applications/<app>`, `/authentication/<variant>`, `/settings/<section>`,
`/components/<name>`, `/blocks/<category>/<name>`.

**Registry names** mirror the route's last segment, namespaced by category,
e.g. block `blocks/crm/revenue-overview` → registry item `crm-revenue-overview`.

**State coverage legend** (see `09-states-modals.md` for the full matrix):
- Flagships (CRM + E-commerce, all 40 pages) ship **E/L/Er/F/Sel** where the
  page has a list/table; **P** only on pages with a plausible permission
  boundary (detail/edit views).
- All other families ship happy-path only in Phase 4; state variants are a
  Phase 5+ backlog item per page, prioritized by traffic (list/table pages
  first).

**Mock data.** Every page must resolve its data from a shared generator in
`lib/mock/`, never invent one-off fixtures inline. Entities referenced across
files: `customers`, `deals`, `contacts`, `companies`, `leads`, `activities`,
`sales-reps`, `orders`, `products`, `inventory`, `categories`, `coupons`,
`payments`, `shipments`, `employees`, `tickets`, `projects`, `tasks`,
`properties`, `patients`, `trades`, `campaigns`, `invoices`, `notifications`,
`files`, `notes`, `messages`, `events`. Each gets exactly one generator file;
families that share a concept (e.g. CRM `deals` and Finance `invoices`) still
get separate entities — don't overload one generator with unrelated shapes.

## Not yet specced

Per `project-context.md` Non-goals: no backend/auth wiring, no i18n, no
builder-export tooling. These specs describe **static, token-driven demo
pages only**.
