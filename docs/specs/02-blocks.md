# 02 — Blocks Catalog

Phase 2. Registry-installable compositions that Phase 3–4 pages are built
*from* — build these before any flagship page. Each is a standalone
registry item (`npx shadcn add <registry-name>` must work once published).

**Entry template:** Registry name · Purpose · Props/config · Composed of ·
Data entity · Used by (forward references to `03`/`04`/`05`).

## `blocks/crm/*`

| Block | Registry name | Purpose | Composed of | Data entity |
|---|---|---|---|---|
| Revenue overview | `crm-revenue-overview` | KPI row + area chart of revenue over time | Card, Chart(Area) | `deals`, revenue timeseries |
| Pipeline | `crm-pipeline` | Two render modes: funnel (stat) and kanban (drag columns) | Card, Chart(Funnel) or Kanban columns | `deals` |
| Lead funnel | `crm-lead-funnel` | Source → conversion funnel chart | Chart(Funnel/Bar) | `leads` |
| Sales performance | `crm-sales-performance` | Leaderboard + rep KPI table | Table, Avatar, Progress | `sales-reps`, `deals` |
| Customer health | `crm-customer-health` | Healthy/At-risk/Critical distribution + list | Chart(Donut), Table, Badge | `customers` |
| Activity feed | `crm-activity-feed` | Chronological timeline of calls/emails/meetings/notes/tasks | List, Avatar, Badge | `activities` |
| Upcoming meetings | `crm-upcoming-meetings` | Compact list of next meetings | Card, List, Avatar | `activities` (meeting type) |
| Recent deals | `crm-recent-deals` | Table of latest deals with stage/value | Table, Badge, Avatar | `deals` |

## `blocks/ecommerce/*`

| Block | Registry name | Purpose | Composed of | Data entity |
|---|---|---|---|---|
| Revenue overview | `ecom-revenue-overview` | KPI row + revenue trend chart | Card, Chart(Area) | `orders` |
| Order summary | `ecom-order-summary` | Order status breakdown (pending/processing/shipped/…) | Card, Badge, Progress | `orders` |
| Top products | `ecom-top-products` | Ranked product list by sales | Table/List, Avatar(image) | `products` |
| Inventory alert | `ecom-inventory-alert` | Low-stock / out-of-stock callouts | Alert, Table | `inventory` |
| Sales funnel | `ecom-sales-funnel` | Visitors → views → cart → checkout → purchase | Chart(Funnel) | derived from `orders` + synthetic traffic |
| Recent orders | `ecom-recent-orders` | Latest orders table | Table, Badge | `orders` |

## Dashboard layout shells (5) — `blocks/layouts/*`

Reusable page skeletons; every flagship/family page picks one and slots
blocks into its regions instead of hand-rolling a grid.

| Shell | Registry name | Region structure |
|---|---|---|
| A — KPI-first | `layout-kpi-first` | Sidebar + Header + 4-up KPI row + 1 large chart + 1 list |
| B — Analytics | `layout-analytics` | KPI row → large area chart → 2-up (bar/pie) → data table |
| C — Split | `layout-split` | KPI row → 2-col (chart / activity feed) → 2-col (table / table) → full-width table |
| D — Dense admin | `layout-dense-admin` | Filter bar → data table → pagination → bulk-action bar |
| E — Executive | `layout-executive` | KPI row (4) → trend chart → 2-col (regional/product) → metrics table |

## Build notes
- Every block accepts data via props (typed against its `lib/mock/<entity>`
  shape) — no block fetches or generates its own data, so the same block can
  be reused with different mock datasets across families in Phase 4/5.
- `blocks/crm/*` and `blocks/ecommerce/*` are the only blocks built in
  Phase 2; family-specific blocks needed in Phase 4 (e.g. a "health score"
  block for Healthcare) are specced inline in `05-dashboards-other-families.md`
  and built only if no existing block covers the need.
