# 03 — CRM Dashboard Suite (Flagship)

Phase 3. Route root: `/dashboards/crm/*`. Each page is a distinct
information architecture — not a reskin. All 20 pages ship on layout shell
+ blocks from `02-blocks.md` plus page-specific composition. State coverage
(E/L/Er/F/Sel/P) per `09-states-modals.md` flagship matrix.

### CRM-01 — Sales Overview
- Route: `/dashboards/crm/sales-overview`
- Purpose: Top-level snapshot of sales performance
- Sections: Header (date range + pipeline filter) → KPI row (Revenue, Deals, Win Rate, Pipeline) → Revenue chart + Pipeline funnel (2-col) → Recent Deals table → Activity feed
- Blocks: `crm-revenue-overview`, `crm-pipeline` (funnel mode), `crm-recent-deals`, `crm-activity-feed`
- Layout shell: A — KPI-first
- Data entities: `deals`, `activities`, `sales-reps`
- States: E, L, Er, F

### CRM-02 — Sales Pipeline
- Route: `/dashboards/crm/sales-pipeline`
- Purpose: Kanban view of deals moving through stages
- Sections: Header + filters → Pipeline value / win-rate KPIs → Kanban columns (Lead, Qualified, Proposal, Negotiation, Won) with column totals
- Blocks: `crm-pipeline` (kanban mode)
- Components: drag/drop cards (deal value, probability, avatar, due date, tags)
- Data entities: `deals`
- States: E, L, Er, Sel (drag-in-progress)

### CRM-03 — Lead Management
- Route: `/dashboards/crm/lead-management`
- Purpose: Table-first lead triage
- Sections: Lead KPIs → Lead sources chart → Filters → Lead table (Lead, Company, Source, Owner, Score, Status, Last contacted, Created)
- Blocks: `crm-lead-funnel`
- Layout shell: D — Dense admin
- Data entities: `leads`
- States: E, L, Er, F, Sel, bulk-actions

### CRM-04 — Lead Detail
- Route: `/dashboards/crm/leads/[id]`
- Purpose: Single-lead deep dive
- Sections: Back link → Company/Person header + status + actions → Contact info → Activity timeline → Notes → Tasks → Deals
- Components: Tabs, Timeline, Card
- Data entities: `leads`, `activities`, `deals`
- States: L, Er, P (permission-denied variant)

### CRM-05 — Customer 360
- Route: `/dashboards/crm/customers/[id]`
- Purpose: Full customer relationship view — tabs + timeline + tables + cards in one page
- Sections: Customer header (avatar, company, status, owner) → KPI row (Revenue, Orders, LTV, Last Activity) → Timeline → Tabs: Deals / Invoices / Tickets / Notes / Contacts
- Data entities: `customers`, `deals`, `activities`, `tickets`
- States: L, Er, P

### CRM-06 — Contacts
- Route: `/dashboards/crm/contacts`
- Purpose: Contact directory
- Sections: Header (search, filters, add contact) → Contact table (Avatar, Name, Company, Email, Phone, Owner, Tags, Last activity)
- Layout shell: D — Dense admin
- Data entities: `contacts`
- States: E, L, Er, F, Sel

### CRM-07 — Companies
- Route: `/dashboards/crm/companies`
- Purpose: Company directory with drill-in
- Sections: Companies KPI row → Company table → Company detail drawer (Sheet)
- Data entities: `companies`
- States: E, L, Er, F

### CRM-08 — Sales Rep Performance
- Route: `/dashboards/crm/rep-performance`
- Purpose: Team leaderboard and quota tracking
- Sections: Team KPIs → Leaderboard → Revenue-by-rep / Deals-by-rep (2-col) → Performance table (Rank, Avatar, Revenue, Deals, Win rate, Quota, Progress)
- Blocks: `crm-sales-performance`
- Data entities: `sales-reps`, `deals`
- States: L, Er

### CRM-09 — Sales Forecast
- Route: `/dashboards/crm/forecast`
- Purpose: Forward-looking revenue projection
- Sections: Forecast KPI → Forecast chart (Committed / Best case / Pipeline) → Rep forecast table
- Data entities: `deals`, `sales-reps`
- States: L, Er, F (by rep/period)

### CRM-10 — Activities
- Route: `/dashboards/crm/activities`
- Purpose: Cross-team activity log
- Sections: Activity filters (Today/Upcoming/Overdue) → Timeline (Call, Email, Meeting, Note, Task types)
- Blocks: `crm-activity-feed`
- Data entities: `activities`
- States: E, L, Er, F

### CRM-11 — Calendar / Meetings
- Route: `/dashboards/crm/calendar`
- Purpose: Meeting scheduling view
- Sections: Calendar toolbar (Month/Week/Day) → Calendar grid → Upcoming meetings sidebar
- Blocks: `crm-upcoming-meetings`
- Data entities: `activities` (meeting type)
- States: L, Er, E (no meetings)

### CRM-12 — Tasks
- Route: `/dashboards/crm/tasks`
- Purpose: Personal task management
- Sections: Task KPIs → My Tasks tabs (Overdue/Today/Upcoming/Completed) → Task table
- Data entities: `tasks`
- States: E, L, Er, F, Sel

### CRM-13 — Customer Support CRM
- Route: `/dashboards/crm/support`
- Purpose: Support-ops view of ticket load
- Sections: Support KPIs (Open Tickets, Response Time, Resolution Time, CSAT) → Ticket table → Agent performance
- Data entities: `tickets`, `sales-reps` (as agents)
- States: E, L, Er, F

### CRM-14 — Customer Success
- Route: `/dashboards/crm/customer-success`
- Purpose: Health-score-driven customer risk view
- Sections: Customer health (Healthy/At risk/Critical) → Health distribution chart → Customer table (Health score, MRR, Renewal, Product usage, NPS) → Recent activity
- Blocks: `crm-customer-health`
- Data entities: `customers`
- States: E, L, Er, F

### CRM-15 — Marketing CRM
- Route: `/dashboards/crm/marketing`
- Purpose: Campaign-to-revenue attribution
- Sections: Campaign KPIs (Leads, Conversions, Cost/Lead, Revenue) → Campaign chart → Campaign table
- Data entities: `campaigns`, `leads`
- States: L, Er, F

### CRM-16 — Email Campaign CRM
- Route: `/dashboards/crm/email-campaigns`
- Purpose: Email-specific funnel
- Sections: Campaign performance KPIs (Sent, Delivered, Opened, Clicked, Converted) → Funnel chart → Campaign table
- Data entities: `campaigns`
- States: L, Er, E

### CRM-17 — Account Management
- Route: `/dashboards/crm/accounts`
- Purpose: Account-level rollup with drill-in
- Sections: Accounts KPI → Accounts table → Account detail (tabs: Contacts, Contracts, Deals, Activities)
- Data entities: `companies`, `deals`, `activities`
- States: L, Er, F, P

### CRM-18 — CRM Analytics
- Route: `/dashboards/crm/analytics`
- Purpose: Cross-cutting analytics with segmentation
- Sections: Header (date range, segments) → Revenue/Pipeline/Conversion KPI row → Multiple charts → Cohort table
- Layout shell: B — Analytics
- Data entities: `deals`, `customers`
- States: L, Er, F

### CRM-19 — CRM Executive Dashboard
- Route: `/dashboards/crm/executive`
- Purpose: Minimal, dense, leadership-facing
- Sections: Revenue/Pipeline/Customers/Retention KPI row → Revenue trend → Sales funnel → Team performance → Risks/alerts
- Layout shell: E — Executive
- Data entities: `deals`, `customers`, `sales-reps`
- States: L, Er

### CRM-20 — CRM Command Center
- Route: `/dashboards/crm/command-center`
- Purpose: "Mission control" — the most composite page in the suite
- Sections: Global search → Critical alerts → Today's Tasks / Pipeline / Meetings / New Leads (4-up) → Recent activity
- Blocks: `crm-activity-feed`, `crm-upcoming-meetings`
- Data entities: `deals`, `leads`, `activities`, `tasks`
- States: L, Er, E (per widget)

## Build notes
- Build order: CRM-01, 02, 03, 05, 06 first (exercise every block from `02-blocks.md` at least once), then the rest in any order.
- CRM-04, 05, 07, 17 are the detail/drawer patterns — reuse one drawer/detail composition across them rather than four bespoke ones.
