# 05 — Other Dashboard Families

Phase 4. Route root: `/dashboards/<family>/*`. 82 pages across 9 families,
built via the same block→page pattern as CRM/E-commerce, reusing
`02-blocks.md` shells and generic KPI/chart/table blocks wherever the
concept transfers (e.g. any "Overview" page = layout shell A + a
family-specific revenue/activity block). Only build a new family-specific
block when nothing existing fits — note it inline where that's expected.

Happy-path only in Phase 4 (no state-variant requirement); see
`09-states-modals.md` for the Phase 5+ backlog once these exist.

## SaaS (10) — `/dashboards/saas/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| SaaS Overview | `overview` | Top-level product/business snapshot | Layout A, Chart(Area) | `customers`, synthetic MRR |
| Product Analytics | `product-analytics` | Feature/event usage over time | Layout B, Chart(Line/Bar) | synthetic usage events |
| MRR Dashboard | `mrr` | Monthly recurring revenue breakdown (new/expansion/churn/contraction) | Waterfall/stacked bar | synthetic MRR |
| Subscription Analytics | `subscriptions` | Plan mix, upgrades/downgrades | Table, Chart(Pie) | `customers` (plan field) |
| Churn Dashboard | `churn` | Churn rate trend + at-risk list | Chart(Line), Table | `customers` |
| Customer Health | `customer-health` | Reuses `crm-customer-health` block | Chart(Donut), Table | `customers` |
| Usage Analytics | `usage` | Per-account usage table + trend | Table, Chart | synthetic usage events |
| Feature Adoption | `feature-adoption` | Adoption funnel per feature | Chart(Funnel/Bar) | synthetic usage events |
| Revenue Analytics | `revenue-analytics` | Revenue breakdown, cohort | Layout B | synthetic MRR |
| SaaS Executive Dashboard | `executive` | Layout E — Executive | KPI row + trend + team | `customers`, synthetic MRR |

## Finance (10) — `/dashboards/finance/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| Finance Overview | `overview` | Layout A — cash position snapshot | KPI row, Chart | `invoices`, synthetic ledger |
| Revenue | `revenue` | Revenue trend + breakdown | Chart(Area/Bar) | synthetic ledger |
| Expenses | `expenses` | Expense categories + trend | Chart(Pie), Table | synthetic ledger |
| Cash Flow | `cash-flow` | Inflow/outflow waterfall | Chart(Bar, diverging) | synthetic ledger |
| Transactions | `transactions` | Full transaction ledger | Layout D — Dense admin | synthetic ledger |
| Invoices | `invoices` | Invoice list + status | Table, Badge | `invoices` |
| Bills | `bills` | Payables list | Table, Badge | synthetic ledger |
| Accounts | `accounts` | Chart of accounts / balances | Table | synthetic ledger |
| Budget | `budget` | Budget vs. actual | Chart(Bar, comparison), Progress | synthetic ledger |
| Financial Reports | `reports` | P&L / balance sheet style tables | Table (grouped rows) | synthetic ledger |

## HR (10) — `/dashboards/hr/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| HR Overview | `overview` | Headcount, hiring, attrition KPIs | Layout A | `employees` |
| Employee Directory | `directory` | Searchable employee table | Layout D | `employees` |
| Employee Profile | `employees/[id]` | See "Profile pages" in `07` | Card, Tabs | `employees` |
| Attendance | `attendance` | Attendance calendar/table | Calendar, Table | synthetic attendance |
| Leave Management | `leave` | Leave requests queue | Table, Badge | synthetic leave requests |
| Payroll | `payroll` | Payroll run table | Table | synthetic payroll |
| Recruitment | `recruitment` | Pipeline of candidates (kanban-like CRM-02 pattern) | Kanban | synthetic candidates |
| Performance | `performance` | Review cycle status + scores | Table, Progress | synthetic reviews |
| Organization | `organization` | Org chart | Tree/nested cards | `employees` |
| HR Analytics | `analytics` | Layout B | Chart, Table | `employees` |

## Project Management (10) — `/dashboards/project-management/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| Project Overview | `overview` | Portfolio snapshot | Layout A | `projects` |
| Project Dashboard | `dashboard` | Single active project's health | KPI row, Chart | `projects`, `tasks` |
| Project List | `projects` | All projects table | Layout D | `projects` |
| Kanban Board | `kanban` | Task board (reuses CRM-02 kanban pattern) | Kanban | `tasks` |
| Task List | `tasks` | Flat task table | Table | `tasks` |
| Calendar | `calendar` | Reuses CRM-11 calendar pattern | Calendar | `tasks`, `events` |
| Timeline / Gantt | `timeline` | Gantt-style project timeline | Custom timeline chart | `projects`, `tasks` |
| Team Workload | `workload` | Per-person allocation | Table, Progress | `employees`, `tasks` |
| Project Reports | `reports` | Burndown/velocity charts | Chart | `tasks` |
| Project Detail | `projects/[id]` | Single project deep dive | Tabs, Timeline | `projects`, `tasks` |

## Support / Helpdesk (10) — `/dashboards/support/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| Support Overview | `overview` | Layout A | KPI row | `tickets` |
| Ticket Inbox | `tickets` | Reuses CRM-13 ticket table pattern | Layout D | `tickets` |
| Ticket Detail | `tickets/[id]` | Single ticket thread | Timeline, Card | `tickets` |
| Customer Profile | `customers/[id]` | Support history for one customer | Tabs | `customers`, `tickets` |
| Agent Dashboard | `agent` | Per-agent queue + KPIs | KPI row, Table | `tickets`, `sales-reps` (as agents) |
| SLA Dashboard | `sla` | SLA compliance tracking | Chart, Progress | `tickets` |
| Knowledge Base | `knowledge-base` | Article list + categories | Accordion, Table | synthetic articles |
| Canned Responses | `canned-responses` | Template management table | Table | synthetic templates |
| Customer Satisfaction | `csat` | CSAT/NPS trend | Chart | `tickets` |
| Support Analytics | `analytics` | Layout B | Chart, Table | `tickets` |

## Healthcare (8) — `/dashboards/healthcare/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| Healthcare Overview | `overview` | Layout A | KPI row | `patients` |
| Patient List | `patients` | Layout D | Table | `patients` |
| Patient Profile | `patients/[id]` | Customer-360-style patient view | Tabs, Timeline | `patients` |
| Appointments | `appointments` | Calendar of appointments | Calendar | `events` |
| Doctor Dashboard | `doctor` | Per-doctor schedule + patient load | KPI row, Table | `patients`, `events` |
| Medical Records | `records` | Record list + detail | Table, Card | `patients` |
| Billing | `billing` | Reuses Finance invoice pattern | Table, Badge | `invoices` |
| Healthcare Analytics | `analytics` | Layout B | Chart, Table | `patients` |

## Real Estate (8) — `/dashboards/real-estate/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| Real Estate Overview | `overview` | Layout A | KPI row | `properties` |
| Properties | `properties` | Property grid/table | Card grid, Table | `properties` |
| Property Detail | `properties/[id]` | Single listing page | Carousel, Card | `properties` |
| Leads | `leads` | Reuses CRM-03 lead table pattern | Layout D | `leads` |
| Agents | `agents` | Reuses CRM-08 rep performance pattern | Table, Avatar | `sales-reps` (as agents) |
| Viewings | `viewings` | Scheduled viewings calendar | Calendar | `events` |
| Deals | `deals` | Reuses CRM-02 pipeline pattern | Kanban | `deals` |
| Real Estate Analytics | `analytics` | Layout B | Chart, Table | `properties`, `deals` |

## Logistics (8) — `/dashboards/logistics/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| Logistics Overview | `overview` | Layout A | KPI row | `shipments` |
| Shipments | `shipments` | Reuses ECOM-16 fulfillment pattern | Layout D | `shipments` |
| Shipment Detail | `shipments/[id]` | Tracking timeline for one shipment | Timeline, Map placeholder | `shipments` |
| Fleet | `fleet` | Vehicle table | Table | synthetic fleet |
| Drivers | `drivers` | Driver directory | Table, Avatar | synthetic drivers |
| Warehouses | `warehouses` | Warehouse list + capacity | Table, Progress | synthetic warehouses |
| Delivery Tracking | `tracking` | Live-style tracking board | Table, Badge | `shipments` |
| Logistics Analytics | `analytics` | Layout B | Chart, Table | `shipments` |

## Cryptocurrency / Trading (8) — `/dashboards/crypto/*`

| Page | Route slug | Purpose | Key components | Data entities |
|---|---|---|---|---|
| Trading Overview | `overview` | Layout A | KPI row | `trades` |
| Portfolio | `portfolio` | Holdings breakdown | Chart(Pie), Table | `trades` |
| Assets | `assets` | Asset list w/ price + change | Table, Badge | `trades` |
| Transactions | `transactions` | Buy/sell/transfer ledger | Layout D | `trades` |
| Market Overview | `market` | Watchlist-style market table | Table, sparkline Chart | `trades` |
| Trading Detail | `trade/[id]` | Single-asset chart + order book | Chart(candlestick), Table | `trades` |
| Wallet | `wallet` | Balance + address list | Card, Table | `trades` |
| Performance | `performance` | P&L over time | Chart(Line) | `trades` |

## Build notes
- Build families in this order: SaaS, Finance, HR (highest pattern reuse
  from CRM/E-commerce), then PM, Support, then Healthcare/Real
  Estate/Logistics/Crypto (most novel, lowest reuse).
- Any page above whose "Key components" cites an existing block
  (`crm-*`/`ecom-*`) must import it, not re-implement it.
