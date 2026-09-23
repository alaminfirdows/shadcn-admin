# 04 — E-commerce Dashboard Suite (Flagship)

Phase 3. Route root: `/dashboards/ecommerce/*`. Covers both store operations
and business analytics. Same template/state rules as `03-dashboards-crm.md`.

### ECOM-01 — Store Overview
- Route: `/dashboards/ecommerce/overview`
- Purpose: Top-level store snapshot
- Sections: KPI row (Revenue, Orders, Customers, Conversion) → Revenue chart + Orders chart (2-col) → Recent orders → Top products
- Blocks: `ecom-revenue-overview`, `ecom-recent-orders`, `ecom-top-products`
- Layout shell: A — KPI-first
- Data entities: `orders`, `products`, `customers`
- States: E, L, Er, F

### ECOM-02 — Sales Analytics
- Route: `/dashboards/ecommerce/sales-analytics`
- Purpose: Revenue composition breakdown
- Sections: Revenue KPIs → Revenue trend → Gross sales / Net sales / Discounts / Refunds (4-up) → Sales table
- Layout shell: B — Analytics
- Data entities: `orders`, `coupons`
- States: L, Er, F

### ECOM-03 — Orders Dashboard
- Route: `/dashboards/ecommerce/orders`
- Purpose: Order queue by status
- Sections: Orders KPI → Status tabs (All/Pending/Processing/Shipped/Delivered/Cancelled) → Orders table
- Layout shell: D — Dense admin
- Data entities: `orders`
- States: E, L, Er, F, Sel, bulk-actions

### ECOM-04 — Order Detail
- Route: `/dashboards/ecommerce/orders/[id]`
- Purpose: Single order deep dive
- Sections: Order # header (customer, payment status, fulfillment status) → Items → Shipping → Billing → Timeline → Actions
- Data entities: `orders`, `customers`
- States: L, Er, P

### ECOM-05 — Products
- Route: `/dashboards/ecommerce/products`
- Purpose: Catalog management table
- Sections: Product KPIs → Search/filters/categories → Product table (Image, Product, SKU, Category, Price, Stock, Status, Sales)
- Layout shell: D — Dense admin
- Data entities: `products`, `categories`
- States: E, L, Er, F, Sel

### ECOM-06 — Product Editor
- Route: `/dashboards/ecommerce/products/[id]/edit`
- Purpose: Major forms showcase — full product authoring
- Sections: Product title → Images uploader → Description → Pricing → Inventory → Shipping → Variants → SEO → Publish
- Components: FieldGroup/Field throughout, InputGroup, multi-section form
- Data entities: `products`
- States: L, Er, validation-error

### ECOM-07 — Inventory
- Route: `/dashboards/ecommerce/inventory`
- Purpose: Stock-level overview
- Sections: Inventory KPIs (Stock value, Low stock, Out of stock) → Inventory table → Stock movement
- Blocks: `ecom-inventory-alert`
- Data entities: `inventory`
- States: E, L, Er, F

### ECOM-08 — Inventory Detail
- Route: `/dashboards/ecommerce/inventory/[id]`
- Purpose: Per-SKU stock history
- Sections: Product header → Current stock → Stock movement timeline → Purchase orders → Warehouse locations → Adjustment form
- Data entities: `inventory`, `products`
- States: L, Er, P

### ECOM-09 — Customers
- Route: `/dashboards/ecommerce/customers`
- Purpose: Customer list with commerce metrics
- Sections: Customer KPIs → Customers table (Segment, Orders, Revenue, LTV, Last purchase)
- Layout shell: D — Dense admin
- Data entities: `customers`, `orders`
- States: E, L, Er, F

### ECOM-10 — Customer Detail
- Route: `/dashboards/ecommerce/customers/[id]`
- Purpose: Single customer commerce history
- Sections: Customer profile → LTV/Orders/Refunds/AOV (4-up) → Order history → Activity → Addresses
- Data entities: `customers`, `orders`
- States: L, Er, P

### ECOM-11 — Categories
- Route: `/dashboards/ecommerce/categories`
- Purpose: Catalog taxonomy management
- Sections: Category tree → Categories table (Products count, Revenue, Actions)
- Data entities: `categories`, `products`
- States: E, L, Er

### ECOM-12 — Discounts / Coupons
- Route: `/dashboards/ecommerce/discounts`
- Purpose: Promotions management
- Sections: Coupon KPIs (Active, Expired, Usage, Revenue) → Coupon table
- Data entities: `coupons`
- States: E, L, Er, F

### ECOM-13 — Marketing
- Route: `/dashboards/ecommerce/marketing`
- Purpose: Campaign performance for the store
- Sections: Campaign KPIs → Campaign performance chart → Revenue attribution → Campaign table
- Data entities: `campaigns`, `orders`
- States: L, Er, F

### ECOM-14 — Conversion Analytics
- Route: `/dashboards/ecommerce/conversion-analytics`
- Purpose: Funnel visualization from traffic to purchase
- Sections: Visitors → Product views → Add to cart → Checkout → Purchase (vertical funnel chart)
- Blocks: `ecom-sales-funnel`
- Data entities: synthetic traffic + `orders`
- States: L, Er

### ECOM-15 — Abandoned Carts
- Route: `/dashboards/ecommerce/abandoned-carts`
- Purpose: Cart-recovery operations view
- Sections: Abandoned carts / Potential revenue / Recovered revenue / Recovery rate (4-up) → Cart table → Recovery actions
- Data entities: `orders` (cart state)
- States: E, L, Er, F

### ECOM-16 — Shipping / Fulfillment
- Route: `/dashboards/ecommerce/fulfillment`
- Purpose: Fulfillment pipeline
- Sections: Orders awaiting fulfillment → Status tabs (Processing/Packed/Shipped/Delivered) → Fulfillment table
- Data entities: `shipments`, `orders`
- States: E, L, Er, F

### ECOM-17 — Returns / Refunds
- Route: `/dashboards/ecommerce/returns`
- Purpose: RMA management
- Sections: Refund KPIs (Amount, Return rate, Pending, Approved) → Returns table → Return detail drawer
- Data entities: `orders` (refund state)
- States: E, L, Er, F

### ECOM-18 — Payments
- Route: `/dashboards/ecommerce/payments`
- Purpose: Payment operations view
- Sections: Payment volume KPIs (Successful/Failed/Refunded/Pending) → Payment method chart → Transactions table
- Data entities: `payments`
- States: E, L, Er, F

### ECOM-19 — Store Analytics
- Route: `/dashboards/ecommerce/store-analytics`
- Purpose: Full-funnel business analytics
- Sections: Revenue/Orders/AOV/Customers/Conversion KPI row → Revenue trend → Top products → Top categories → Customer cohorts
- Layout shell: B — Analytics
- Data entities: `orders`, `products`, `categories`, `customers`
- States: L, Er, F

### ECOM-20 — E-commerce Command Center
- Route: `/dashboards/ecommerce/command-center`
- Purpose: Operator's home screen — most composite page in the suite
- Sections: Today's revenue → Orders requiring attention → Low stock → Failed payments → Pending fulfillment → Refund requests → Customer issues → Sales alerts
- Blocks: `ecom-inventory-alert`, `ecom-recent-orders`
- Data entities: `orders`, `inventory`, `payments`, `shipments`, `tickets`
- States: L, Er, E (per widget)

## Build notes
- Build order: ECOM-01, 03, 05, 09 first (exercise every block from `02-blocks.md`), then the rest.
- ECOM-04, 08, 10 share one order/detail-drawer composition pattern with CRM-04/05/07 — build it once, reuse across both suites.
- ECOM-06 (Product Editor) is the primary vehicle for the Form gallery patterns in `08-data-tables-forms-charts.md` — build after that file's "multi-section form" pattern is defined.
