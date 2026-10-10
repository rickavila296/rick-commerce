# Rick-Commerce

An open e-commerce starter for a school, office and art supplies store, built on a plain PERN stack: PostgreSQL, Express, React and Node, with TypeScript throughout. Fork it and adapt it to your own catalogue.

> **Disclaimer.** Rick-Commerce is a demonstration project. Its sample catalogue is modelled on the product range of AMSPEC (Amalgamated Specialties Corporation), a Philippine school-supplies company. This project is not affiliated with, endorsed by or connected to AMSPEC or any brand named in it. Brand names appear as plain text for identification only. Every product, price and stock level is invented. No real orders are taken and no real payments are processed.

## Status

Early development. The repository currently contains the project setup, the local database and the decision log. Application code is being added; the features below are the design target, not a list of what works today.

## What it is designed to do

| Area | Design |
| --- | --- |
| Catalogue | Categories, products with variants (pack sizes), search, filters, sorting and pagination, with all list state in the URL |
| Cart | Server-side cart for guests and customers, merged at login; prices always computed on the server |
| Checkout | Single-page checkout; order placement in one database transaction that cannot oversell stock |
| Payments | Card, GCash, Maya, QR Ph and cash on delivery through a mock provider behind one interface, with signed webhooks, retries and expiry |
| Refunds | Customer cancellation before shipping; automatic and manual refund paths |
| Admin | Catalogue, inventory with a movement ledger, order fulfilment, and four fixed staff roles |
| Bulk orders | A quote inquiry form with an admin inbox |

## Tech stack

| Layer | Choice |
| --- | --- |
| Language | TypeScript, strict mode, client and server |
| API | Node.js, Express 5, REST over JSON |
| Database | PostgreSQL with hand-written, parameterized SQL and versioned migrations |
| Auth | Server-side sessions in an HttpOnly cookie, Argon2id password hashing |
| Frontend | React with Vite, React Router, TanStack Query, Tailwind CSS |
| Testing | Vitest and Supertest against a real PostgreSQL database |

## Requirements

- Node.js LTS (built with v24)
- Docker Desktop
- Git

## Getting started

```bash
git clone https://github.com/rickavila296/rick-commerce.git
cd rick-commerce
cp .env.example .env
npm run db:up
npm run db:psql
```

`db:psql` opens a PostgreSQL prompt inside the container. Type `\q` to leave.

| Script | What it does |
| --- | --- |
| `npm run db:up` | Start PostgreSQL in Docker |
| `npm run db:stop` | Stop it and keep the data |
| `npm run db:reset` | Delete all data and start an empty database |
| `npm run db:psql` | Open a psql prompt in the database |

## Structure

```
client/               React app (Vite)
server/               Express API
docs/                 Decision log
docker-compose.yml    PostgreSQL for local development
.env.example          Configuration names; copy to .env
```

`client` and `server` are separate apps, each with its own dependencies. The only thing they share is the HTTP API.

## Documentation

Significant design decisions are recorded in [`docs/decision-log.md`](docs/decision-log.md), each with the options considered, the reason and the consequences.

## Images

No real product photographs, logos or packaging are used. Product images are generated placeholders.

## Adapting it

- Replace the store name, the seed catalogue and the brand names with your own.
- Keep or reword the disclaimer to match what your store actually is.
- Payments run against a mock provider. A real provider is added by writing one adapter for the payment interface.

## Licence

Released under the [MIT Licence](LICENSE). You may use, change and redistribute the code as long as the copyright notice is kept. The licence covers the code in this repository only; it grants no rights to the third-party brand names mentioned in it.
