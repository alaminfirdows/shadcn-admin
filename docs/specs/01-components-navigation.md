# 01 — Component Showcase & Navigation Patterns

Phase 1. Route root: `/components/*` and `/components/navigation/*`.
Every entry below is a real-world composition page, not a bare prop-toggle
demo — each shows the component used the way a real app would use it.

## Primitive showcase pages (one route per component)

For each shadcn primitive, ship a `/components/<name>` page with the target
number of real-world composition examples listed. Full breakdowns are given
below only for the components the spec calls out explicitly (Button,
Sidebar, Header); the rest follow the same depth pattern — 6–10 compositions
each, covering states (default/disabled/loading), density, and at least one
"used inside a real block" example.

| Component | Target compositions | Notes |
|---|---:|---|
| Accordion | 6 | single/multiple open, FAQ style, settings group |
| Alert | 6 | info/success/warning/destructive, with actions, dismissible |
| Avatar | 6 | with fallback, group/stack, status dot, sizes |
| Badge | 8 | status, count, dot, removable, semantic-color variants only |
| Breadcrumb | 6 | truncated, with dropdown overflow, icon leading |
| Button | 15 | see full list below |
| Calendar | 6 | single, range, with disabled dates, inline in popover |
| Card | 8 | full composition (header/title/description/content/footer), stat card, list card |
| Carousel | 5 | image, testimonial, product, with dots, with thumbnails |
| Chart | — | full gallery in `08-data-tables-forms-charts.md` |
| Checkbox | 6 | single, group, indeterminate, with description |
| Command | 6 | command palette, inline search, with groups/shortcuts |
| Context Menu | 5 | table row, file item, with submenu |
| Data Table | — | full gallery in `08-data-tables-forms-charts.md` |
| Date Picker | 6 | single, range, with presets, inline |
| Dialog | — | full gallery in `09-states-modals.md` |
| Drawer | — | full gallery in `09-states-modals.md` |
| Dropdown Menu | 8 | actions menu, with checkboxes, with submenu, user menu |
| Input | 8 | with icon, with addon, validation states, OTP-adjacent |
| Menubar | 4 | app-style top menu |
| Pagination | 6 | numbered, simple prev/next, with page size select |
| Popover | 5 | form-in-popover, info popover, color/date pickers |
| Progress | 5 | linear, with label, multi-step, indeterminate |
| Radio Group | 5 | list, card-style options, with description |
| Resizable | 4 | two-pane, three-pane, with min/max |
| Select | 6 | single, grouped, searchable (Combobox), multi via ToggleGroup |
| Sheet | — | full gallery in `09-states-modals.md` |
| Sidebar | 15 | see navigation section below |
| Skeleton | 6 | card, table, list, avatar+text, chart |
| Slider | 5 | single, range, with steps/marks |
| Spinner | 4 | inline, button, overlay, full-page |
| Switch | 5 | single, with label/description, settings row |
| Table | — | full gallery in `08-data-tables-forms-charts.md` |
| Tabs | 6 | underline, pill, with badge counts, vertical |
| Textarea | 4 | auto-resize, with counter, disabled |
| Toast (sonner) | 8 | success/error/info/loading, with action, promise-based |
| Toggle / Toggle Group | 6 | icon-only, text, single vs multi-select |
| Tooltip | 4 | icon-only trigger, keyboard shortcut hint, on disabled control |
| Typography | 6 | full scale (h1–h4, lead, muted, code, blockquote) |

**Button — full 15-item composition list** (reference depth for all others):
Primary · Secondary · Destructive · Outline · Ghost · Link · Icon-only ·
Icon + text · Loading · Disabled · Split button · Button group · Dropdown
button · Copy button (with copied-state) · Delete-with-confirmation.

## Navigation gallery — `/components/navigation/*`

### Sidebar variants (15) — route `/components/navigation/sidebar/<n>`
1. Simple sidebar (flat links)
2. Collapsible sidebar (expand/collapse rail)
3. Icon-only sidebar (rail mode)
4. Sidebar with nested navigation (2-level)
5. Sidebar with badges (counts/status dots on items)
6. Sidebar with teams switcher
7. Sidebar with workspace switcher
8. Sidebar with projects list
9. Sidebar with bottom user menu (avatar + dropdown)
10. Sidebar with command search (⌘K trigger)
11. Sidebar with pinned items
12. Sidebar with favorites section
13. Multi-level navigation (3+ levels)
14. Mobile drawer navigation (Sheet-based)
15. RTL sidebar

Each variant: Route, Components (Sidebar primitive + composed pieces),
Data entity (`nav-items` mock), Phase 1.

### Header variants (11) — route `/components/navigation/header/<n>`
1. Simple header (title only)
2. Breadcrumb header
3. Search header (inline search field)
4. Header + actions (buttons on the right)
5. Header + date range picker
6. Header + tabs (section switcher)
7. Header + workspace switcher
8. Header + notifications (bell + popover)
9. Sticky header (scroll behavior)
10. Full-width header (no max-width container)
11. Mobile header (hamburger + condensed actions)

## Build notes
- Sidebar/header variants become the literal building blocks the flagship
  dashboards (`03`, `04`) pick from — do not fork them per dashboard, import
  the composed component.
- `@shadcn/lint` (`no-restyle`, `no-arbitrary-values`) applies to every file
  in this phase; this is the first real test of the token-discipline rules.
