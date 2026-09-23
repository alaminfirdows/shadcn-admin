# 07 — Authentication, Settings, Profile

Phase 5. All static/non-functional — forms render and validate client-side
only, no real auth flow.

## Authentication (15) — `/authentication/*`

Standard split layout: brand/artwork + quote (left) — form (right), per the
plan's reference composition. Route = `/authentication/<slug>`.

| # | Variant | Slug | Key elements |
|---|---|---|---|
| 1 | Login | `login` | Email, password, remember me, forgot-password link, social buttons |
| 2 | Signup | `signup` | Name, email, password, confirm, terms checkbox |
| 3 | Forgot Password | `forgot-password` | Email input, submit → confirmation state |
| 4 | Reset Password | `reset-password` | New password, confirm, strength indicator |
| 5 | Verify Email | `verify-email` | Info panel + resend action, no form |
| 6 | Magic Link | `magic-link` | Email input → "check your inbox" state |
| 7 | Two-factor authentication | `two-factor` | 6-digit code input, resend timer |
| 8 | OTP | `otp` | InputOTP component, auto-submit on complete |
| 9 | Passkey | `passkey` | "Continue with passkey" CTA + platform icon |
| 10 | Social login | `social-login` | Grid of provider buttons (Google/GitHub/etc.) |
| 11 | Invite acceptance | `invite` | Inviter info card + accept/decline |
| 12 | Organization selection | `select-organization` | Card list of orgs to switch into |
| 13 | Workspace selection | `select-workspace` | Card list of workspaces |
| 14 | Account recovery | `account-recovery` | Recovery-code input |
| 15 | SSO login | `sso` | Domain/email input → redirect-style CTA |

- Components: Field/FieldGroup, Input, InputOTP, Checkbox, Alert (errors), Button (loading state on submit)
- Data entities: none (client-only form state)
- States: validation-error, submitting, success/confirmation per variant

## Settings (17 sections) — `/settings/*`

One settings app shell (sidebar or tabs nav) with 17 section routes, each
demonstrating a distinct form pattern per the `shadcn` skill's forms rules
(FieldGroup/Field, no raw div+space-y).

| # | Section | Slug | Form pattern demonstrated |
|---|---|---|---|
| 1 | General | `general` | Simple single-column form |
| 2 | Profile | `profile` | Avatar upload + basic fields |
| 3 | Account | `account` | Email/username change with confirmation |
| 4 | Appearance | `appearance` | Theme + token-theme picker (ToggleGroup) |
| 5 | Notifications | `notifications` | Grouped Switch list (FieldSet/FieldLegend) |
| 6 | Security | `security` | 2FA toggle, security overview cards |
| 7 | Password | `password` | Current/new/confirm, strength meter |
| 8 | Sessions | `sessions` | Active sessions table + revoke action |
| 9 | API Keys | `api-keys` | Key table + create-key dialog with copy-once reveal |
| 10 | Integrations | `integrations` | Card grid of connect/disconnect integrations |
| 11 | Billing | `billing` | Plan card + invoice table + payment method |
| 12 | Team | `team` | Member table + invite dialog |
| 13 | Roles | `roles` | Role list + permission matrix table |
| 14 | Permissions | `permissions` | Checkbox matrix (FieldSet) |
| 15 | Domains | `domains` | Domain table + verify-DNS flow |
| 16 | Webhooks | `webhooks` | Webhook table + endpoint form + delivery log |
| 17 | Danger Zone | `danger-zone` | Destructive actions behind AlertDialog confirmation |

- Data entities: reuses `customers`/`employees` shape for the acting user; `payments`/`invoices` for Billing
- States: saving, saved-toast, validation-error, empty (Sessions/API Keys/Webhooks before first item)

## Profile pages (3) — `/profile/*`

| Variant | Route | Sections |
|---|---|---|
| User profile | `/profile/user` | Avatar, name, role, email → About → Activity → Projects → Teams → Recent activity |
| Public profile | `/profile/public/[handle]` | Cover + avatar → Name, bio, social links → Projects → Posts → Activity |
| Employee profile | `/dashboards/hr/employees/[id]` | Employee, department, manager → Contact → Employment → Projects → Leave → Performance (cross-referenced from HR family, `05`) |

- Components: Card, Tabs, Avatar, Badge
- Data entities: `customers`/`employees`, `activities`, `projects`

## Build notes
- Auth pages ship first in this file — they're pure form/layout exercises
  with no data dependency, good warm-up before Settings' more complex forms.
- Settings' Billing/Team/Roles/Permissions sections are the most
  composition-heavy; build after the Data Table and Form galleries
  (`08-data-tables-forms-charts.md`) so their patterns are already defined.
