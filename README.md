# Muhammad Ibrahim

**Full-stack developer — Odoo ERP · PostgreSQL · Supabase · TypeScript**
📍 Pakistan (UTC+5 — full overlap with EU, morning overlap with US East) · 🌍 **Open to remote, worldwide**

I build business software that has to be *correct*: double-entry ledgers, ERP
customisation, and integrations that keep two systems in sync without ever
losing or duplicating a record.

Available for **remote roles and contract work** (W-8BEN, EoR-friendly — Deel, Remote.com).

---

## 📦 Open source

### [**odoo-shopify-connector**](https://github.com/asim98-aseem/odoo-shopify-connector) — run it yourself with `docker compose up`

Two-way Odoo 19 ↔ Shopify sync over the Admin **GraphQL** API. Built around the
three things that actually break Shopify integrations in production, each with a
test that fails if the guard is removed:

- **Shopify returns HTTP 200 for rejected writes** — the client raises on
  `userErrors`, so a failed push can't be logged as a success.
- **The rate limit is cost-based** — it reads `throttleStatus` and computes the
  real backoff, `(1000−50)/100 = 9.5s`, rather than sleeping on a guess.
- **Delivery is at-least-once** — every write path is idempotent, guarded by
  database unique indexes rather than app-level check-then-create, because only
  an index can arbitrate two workers racing the same retry.

Plus HMAC-verified webhooks (constant-time compare, with a test that fails if
someone swaps it for `==`), multi-store, multi-company, and CI that runs both an
Odoo-free unit suite and full Odoo integration tests on a real PostgreSQL.

`19 integration tests` · `37 unit tests` · `MIT`

---

## What I've built

### 🛠 Jewellery ERP on Odoo 19
A production ERP for a luxury jewellery manufacturer — 3 custom addons, **47 models**.

- **Product & variant engine** — 70+ jewellery-specific fields on `product.template`; material
  combinations resolve into native Odoo attributes, then into sellable variants with
  auto-generated SKUs and QR codes.
- **Shopify sync** — GraphQL Admin API (2026-01): pushes products, variants, 14+ metafields,
  media, collections, SEO and tags; imports orders and customers.
- **WhatsApp notifications** — Meta Cloud API, auto-firing on order confirmed, production
  started/complete, and delivered.
- **7 analytics dashboards** — catalogue, production, returns, repairs, metal pricing,
  stage performance, inventory.

`Odoo 19` `Python 3.12` `PostgreSQL 15` `GraphQL` `Docker Compose`

### 🌾 Offline-first farm ERP
A field-operations and accounting platform for smallholder farms — **513 commits** and counting.

- **Double-entry general ledger** that stays invisible to the user. Journals are append-only
  and hash-chained, so a tampered row breaks the chain and the audit catches it.
- **Row-level security per organisation**, enforced in PostgreSQL rather than in the app —
  with the narrow ledger policies protected against being widened by later migrations.
- **Offline-first as a guarantee, not a feature.** Every mutation goes through an outbox
  carrying a `client_op_id`; every posting RPC has an idempotency guard, so a retry on a
  patchy rural connection can never post the same transaction twice.
- **CI as the acceptance environment** — every push replays the full migration history into
  a fresh Postgres and runs the suite. No "works on my machine".

`React` `TypeScript` `Supabase` `PostgreSQL` `Vite` `Vitest` `Vercel` `GitHub Actions`

> These two are private client/commercial repos — happy to walk through the architecture,
> the schema, or any of the code on a call.

---

## Stack

| | |
|---|---|
| **Languages** | Python · TypeScript · JavaScript · SQL (PL/pgSQL) |
| **Backend** | Odoo · PostgreSQL · Supabase · Serverless functions · REST & GraphQL |
| **Frontend** | React · Next.js · Vite · Tailwind · shadcn/ui |
| **Data** | Schema design · migrations · row-level security · double-entry accounting |
| **Integrations** | Shopify GraphQL Admin API · Meta WhatsApp Cloud API · webhooks |
| **Infra** | Docker & Docker Compose · Vercel · GitHub Actions CI |

---

## Get in touch

- ✉️ **ibrahimasimec@gmail.com**
- 💬 Open to: full-time remote · contract · Odoo implementation & integration work
