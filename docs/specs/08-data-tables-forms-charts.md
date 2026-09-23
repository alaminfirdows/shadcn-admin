# 08 — Data Table, Form, and Chart Galleries

Phase 5 (build early in Phase 5 — Settings, ECOM-06, and several family
pages depend on the patterns defined here). Route roots: `/components/tables/*`,
`/components/forms/*`, `/components/charts/*`.

## Data Table gallery (15) — `/components/tables/<n>`

| # | Variant | What it demonstrates |
|---|---|---|
| 1 | Basic table | Static rows, no interactivity |
| 2 | Searchable table | Client-side text filter input |
| 3 | Sortable table | Column-header sort (asc/desc) |
| 4 | Filterable table | Faceted filter popovers per column |
| 5 | Column visibility | Dropdown to toggle columns |
| 6 | Row selection | Checkbox column + select-all |
| 7 | Bulk actions | Action bar appears on selection |
| 8 | Expandable rows | Row expands to reveal sub-content |
| 9 | Row actions | Trailing DropdownMenu per row |
| 10 | Grouped rows | Rows grouped by a column with subtotal headers |
| 11 | Nested table | Table inside an expanded row |
| 12 | Table + drawer | Row click opens a Sheet with detail |
| 13 | Table + detail panel | Split view, selected row shown in side panel (Resizable) |
| 14 | Server-side pagination | Page-by-page fetch simulation against mock data |
| 15 | Dense enterprise table | Compact row height, sticky header, many columns |

- Base: TanStack Table + shadcn `Table`/`data-table` primitives.
- Every flagship dashboard table (CRM/E-commerce list pages) must pick one
  of these 15 as its base pattern, not invent a new one.

## Form gallery

### Layouts (11) — `/components/forms/layouts/<n>`
Single column · Two column · Three column · Sidebar form · Card form ·
Wizard (multi-step, linear) · Stepper (multi-step, non-linear with progress
indicator) · Modal form (Dialog) · Drawer form (Sheet) · Inline editing
(click-to-edit cell/field) · Settings form (label-left, control-right rows).

- All use `FieldGroup`/`Field` per the `shadcn` skill's forms rules — no
  raw `div` + `space-y-*`.

### Real-world examples (13) — `/components/forms/examples/<n>`
User creation · Customer creation · Product creation · Employee creation ·
Company creation · Invoice creation · Payment method · Address · Checkout ·
Profile · API key · Integration · Notification settings.

- Each example: Route, which layout pattern it uses, validation rules
  (required/format), and which flagship page (if any) it's extracted from —
  e.g. "Product creation" backs ECOM-06's field sections.

## Charts gallery — `/components/charts/*`

### Basic (8)
Line · Area · Bar · Horizontal bar · Pie · Donut · Radial · Scatter.

### Advanced (11)
Multi-series · Stacked bar · Stacked area · Combo chart (bar+line) ·
Comparison chart (period-over-period) · KPI + sparkline · Goal chart
(progress-to-target) · Funnel · Cohort (heatmap-table hybrid) · Heatmap ·
Timeline chart.

### Real-world examples (9)
Revenue · MRR · Orders · Users · Conversion · Retention · Traffic ·
Expenses · Profit — each wraps one Advanced/Basic chart type with a
domain-labeled dataset, used as the literal chart inside `crm-revenue-overview`,
`ecom-revenue-overview`, and the family dashboards in `05`.

- Base: shadcn `Chart` (Recharts wrapper). All colors from the semantic
  chart-color tokens (`--chart-1..5`), never raw hex — enforced by
  `@shadcn/lint` `no-raw-colors`.

## Build notes
- Build order within this file: Data Table basics (1–7) → Form layouts →
  Charts basics → Data Table advanced (8–15) → Form real-world examples →
  Charts advanced/real-world.
- This file's output directly unblocks: ECOM-06 (forms), all "Dense admin"
  layout-shell pages (tables), and every KPI-chart block in `02-blocks.md`.
