# 10 — Marketing Pages & Section Library

Phase 5. Route root: `/marketing/*`. The one area of the repo that is
explicitly non-dashboard UI — full-bleed, content-first pages composed from
the section library below.

## Landing pages (3) — `/marketing/<slug>`

| Page | Slug | Sections (top → bottom) |
|---|---|---|
| SaaS landing | `saas` | Navbar → Hero → Trusted-by logos → Features → Feature showcase → Testimonials → Pricing → FAQ → CTA → Footer |
| Product landing | `product` | Navbar → Hero → Product screenshot → Features → Use cases → Comparison table → Testimonials → Pricing → FAQ → CTA → Footer |
| Developer landing | `developer` | Navbar → Hero → Code example block → Features → Architecture diagram → Integrations → GitHub CTA → FAQ → Footer |

## Marketing section library — `/blocks/marketing/<category>/<n>`

Each section is independently registrable (`marketing-hero-*`,
`marketing-features-*`, etc.) so the 3 landing pages above are pure
compositions of these, same principle as `02-blocks.md`.

### Hero (7)
Centered hero · Split hero (copy + image) · Product-screenshot hero · Video
hero · Gradient hero · Minimal hero · Dark hero.

### Features (6)
3-column · 4-column · Bento (cross-ref Bento gallery below) · Feature +
screenshot · Alternating feature rows · Icon grid.

### Pricing (6)
3 plans · 4 plans · Monthly/yearly toggle · Enterprise-plan callout ·
Feature-comparison table · Usage-based pricing (slider/calculator).

### Testimonials (5)
Single testimonial · Grid · Carousel · Quote + avatar · Company-logo wall.

### FAQ (3)
Accordion (single column) · Two-column FAQ · Categorized FAQ (tabs +
accordion).

## Bento gallery (8) — `/components/bento/<n>`
2-column · 3-column · Asymmetric · Feature-focused · Metrics-focused ·
Product-showcase · Integrations-focused · Testimonials-focused.

- Components throughout: Card, Badge, Avatar, Carousel, Accordion, Tabs,
  Chart (for metrics-focused bento cells).
- Data entities: none required — marketing copy/logos are static content,
  not generator-driven mock data (unlike the dashboard families).

## Build notes
- Build the section library before the 3 landing pages; landing pages are
  pure composition once sections exist.
- This file has the least dependency on `lib/mock/` of any spec file — safe
  to build in parallel with any other Phase 5 file if needed.
