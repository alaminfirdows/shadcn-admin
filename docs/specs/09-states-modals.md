# 09 — States Gallery, Flagship State Matrix, Modals & Drawers

## Part A — Flagship state matrix (Phase 3, ships with CRM/E-commerce)

Every CRM/E-commerce list or table page already lists its required states
inline in `03-dashboards-crm.md` / `04-dashboards-ecommerce.md`. Summary of
the legend used there:

| Code | Meaning | Implementation |
|---|---|---|
| E | Empty | `Empty` component, e.g. "No customers yet — Start by adding your first customer. [Add Customer]" |
| L | Loading | `Skeleton` matched to the page's actual layout (not a generic spinner) |
| Er | Error | `Alert` (destructive) with retry action |
| F | Filtered-empty | `Empty` variant: "No results found — Try changing your filters." |
| Sel | Selection | Bulk-action bar appears when rows selected |
| P | Permission | "You don't have access — Contact your administrator." panel, used on detail/edit routes only |

Each flagship page component must accept a `state` prop (or read from a
route search-param in the demo) so all variants are reachable without
separate pages, e.g. `/dashboards/crm/customers/[id]?state=permission-denied`.

## Part B — Generic states gallery (Phase 5, for all non-flagship pages)

Route root `/states/*`. Backlog note: once a family page in
`05-dashboards-other-families.md` needs a specific state, wire it using
these same components rather than building new ones.

### Empty states — `/states/empty/<n>`
1. No data ("No customers yet")
2. No search results
3. No integration connected (e.g. "Connect Stripe")
4. Permission denied

### Loading states — `/states/loading/<n>`
1. Skeleton (generic block)
2. Spinner
3. Inline loading (within a row/field)
4. Button loading
5. Table loading
6. Chart loading
7. Card loading
8. Full-page loading

### Error states — `/states/error/<n>`
1. Page error
2. API error
3. Network error
4. Empty-data error (data expected but malformed)
5. Permission error
6. Validation error (form-level)
7. 404
8. 403
9. 500
10. Payment failure
11. Upload failure

- Components throughout: `Empty`, `Skeleton`, `Spinner`, `Alert`, `sonner` toast.
- Data entities: none — these are pure UI states, no data dependency.

## Part C — Modal / Drawer gallery (13) — `/components/overlays/<n>`

Phase 5. Realistic, task-specific overlays (not prop-toggle demos).

1. Delete confirmation (AlertDialog)
2. Create customer (Dialog, form)
3. Edit profile (Dialog, form)
4. Filter panel (Sheet, faceted filters)
5. Command menu (Command inside Dialog, ⌘K)
6. Invite team member (Dialog, email + role select)
7. Share document (Dialog, link + permission select)
8. Payment (Dialog, form)
9. Checkout (Sheet, multi-section)
10. Image preview (Dialog, media-only)
11. Detail drawer (Sheet, read-only record view)
12. Confirmation dialog (generic AlertDialog)
13. Warning dialog (AlertDialog, destructive-adjacent but recoverable)

- Every Dialog/Sheet/Drawer here must include a Title (`sr-only` if visually
  hidden) per the `shadcn` skill's composition rules.
- Cross-reference: #1 backs every flagship "delete" row action; #4 backs
  every "Dense admin" layout shell's filter bar; #11 backs CRM-07/ECOM-17's
  detail drawers.

## Build notes
- Build Part C's #1, #2, #4, #11 first — those four unblock the most
  flagship pages.
- Part B is intentionally last-priority; it exists so non-flagship families
  have a state to reach for once they get a state-coverage pass, not as a
  Phase 5 deliverable in itself.
