# ShopSphere 🛒

A modern full-stack e-commerce platform built with Next.js and Express, featuring authentication, product management, shopping cart functionality, Stripe payments, order tracking, an admin dashboard, and real-time customer support.

![ShopSphere homepage](assets/screenshots/homepage.png)


## Screenshots

### ShopSphere

| Home | Product detail |
| --- | --- |
| ![Homepage](assets/screenshots/homepage.png) | ![Product detail](assets/screenshots/product_detail.png) |

| Cart | Checkout |
| --- | --- |
| ![Cart](assets/screenshots/cart.png) | ![Payment](assets/screenshots/payment.png) |

| Sign in | Sign up |
| --- | --- |
| ![Sign in](assets/screenshots/sign-in.png) | ![Sign up](assets/screenshots/sign-up.png) |

| Your orders | Track order |
| --- | --- |
| ![Your orders](assets/screenshots/your_orders.png) | ![Track your order](assets/screenshots/track_your_order.png) |

| Customer chat |
| --- |
| ![User chat](assets/screenshots/user_chat.png) |

### Admin dashboard

| Overview | Products |
| --- | --- |
| ![Dashboard overview](assets/screenshots/dashboard_overview.png) | ![Products dashboard](assets/screenshots/products_dashboard.png) |

| Analytics | Inventory |
| --- | --- |
| ![Analytics](assets/screenshots/analytics_dashboard.png) | ![Inventory](assets/screenshots/inventory_dashboard.png) |

| Attributes | Reports |
| --- | --- |
| ![Attributes](assets/screenshots/attributes_dashboard.png) | ![Reports](assets/screenshots/reports_dashboard.png) |

| Logs | Admin chat |
| --- | --- |
| ![Logs](assets/screenshots/logs_dashboard.png) | ![Dashboard chat](assets/screenshots/dashboard_chat.png) |

## Features

- **Storefront** — catalog, product detail, cart, Stripe checkout, order tracking
- **Auth** — sign-up, sign-in, roles (user, admin, superadmin)
- **Admin** — products, inventory, attributes, analytics, reports, audit logs
- **Real-time chat** — customer support (Socket.IO)
- **API** — Express + Prisma, PostgreSQL, Redis, Swagger at `/api-docs`
- **Dev experience** — Docker Compose, seed data, env starter docs


## 🏗️ Architecture

ShopSphere is a modern full-stack e-commerce platform built with a Next.js frontend and an Express + Prisma backend. It includes product browsing, shopping cart functionality, Stripe payments, order management, an admin dashboard, Redis caching, and real-time customer support using Socket.IO.

- **Frontend:** Next.js, TypeScript, Tailwind CSS, Redux Toolkit
- **Backend:** Node.js, Express, TypeScript
- **Database:** PostgreSQL with Prisma ORM
- **Caching:** Redis
- **Real-Time Communication:** Socket.IO
- **Payments:** Stripe
- **Media Storage:** Cloudinary

## Project layout

```
src/
  client/     Next.js frontend
  server/     Express API + Prisma
  docker-compose.yml
  .env.example   Docker Postgres credentials (copy to .env)
```

## Local setup

Prerequisites: Node.js 18+, PostgreSQL, Redis (or use Docker).

No cloud database (Neon, etc.) is required for local Docker — Postgres and Redis run in Compose.

1. Clone and go to the repo root.

2. Create environment files (see [src/ENV_STARTER.md](src/ENV_STARTER.md) for a full starter pack):

```
cp src/.env.example src/.env
cp src/server/.env.example src/server/.env
cp src/client/.env.example src/client/.env.local
```

3. Edit the env files before the first `docker compose up`:

| File | Purpose |
|------|---------|
| `src/.env` | Postgres user, password, and database name for the `db` container |
| `src/server/.env` | API secrets, `REDIS_URL`, Stripe/OAuth placeholders, etc. |
| `src/client/.env.local` | `NEXT_PUBLIC_*` URLs pointing at `http://localhost:5000` |

Use the same Postgres password in `src/.env` and in `src/server/.env` `DATABASE_URL` (same user and database name). Example `DATABASE_URL` for Docker:

`postgresql://YOUR_USER:YOUR_PASSWORD@localhost:5432/b2c_ecommerce` (host) — inside Compose, `DATABASE_URL` is overridden to use host `db`.

### Option A — Docker (recommended)

From `src/`:

```
docker compose up --build
```

In a **second terminal**, after containers are running:

```
cd src
docker compose exec server npx prisma migrate deploy
docker compose exec server npm run seed
```

Open http://localhost:3000 (frontend), http://localhost:5000/api/v1 (API), http://localhost:5000/api-docs (Swagger).

### Option B — without Docker

```
cd src/server
npm install
npx prisma migrate dev
npm run seed
npm run dev
```

In another terminal:

```
cd src/client
npm install
npm run dev
```

## Test accounts (after seeding)

After `npm run seed` (or `docker compose exec server npm run seed`). Use only in local development.

| Role       | Email                    | Password      |
|------------|--------------------------|---------------|
| Superadmin | superadmin@example.com | password123   |
| Admin      | admin@example.com      | password123   |
| User       | user@example.com       | password123   |

## More docs

- [src/ENV_STARTER.md](src/ENV_STARTER.md) — copy-paste env values for a fresh clone
- [src/server/README.md](src/server/README.md) — server details
- [src/client/README.md](src/client/README.md) — client details

