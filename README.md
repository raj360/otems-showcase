# OTEM

Public showcase for OTEM, Work-order and fleet operations platform.

## Problem statement

Field and shipping operations tracked jobs through email and spreadsheets. Supervisors needed one system to create work orders, assign staff and assets, track daily progress, share status with clients, and report operational KPIs without rebuilding Excel packs every week.

## Solution path

1. **Single work-order lifecycle:** capture NEW jobs, plan services and resources, move through IN_PROGRESS, then COMPLETE or CANCELLED.
2. **Daily execution:** assign tasks, log progress, track ETAs, and require reasons when deadlines slip.
3. **Two portals:** admin for internal ops, client portal for read-only progress and reporting.
4. **Fleet awareness:** integrate asset systems (Fleetio) so assignments respect equipment reality.
5. **KPI layer:** map TEPU-style ops records into dashboards management can act on.

## Tech stack

| Area | Choices |
| --- | --- |
| Admin and client apps | Next.js, TypeScript, Tailwind, React Relay |
| API | NestJS, GraphQL (Apollo), TypeORM |
| Database | PostgreSQL |
| Monorepo | Yarn workspaces, Turborepo |
| Integrations | Fleetio API |
| Deploy pattern | Vercel for web apps, Railway for API |

## Architecture (clean plan)

```
┌──────────────┐   ┌──────────────┐
│ Admin (Next) │   │ Client (Next)│
│ Relay UI     │   │ read-only UI │
└──────┬───────┘   └──────┬───────┘
       │                  │
       └────────┬─────────┘
                ▼
       ┌────────────────┐
       │ NestJS GraphQL │
       │ work orders ·  │
       │ tasks · staff  │
       │ assets · KPIs  │
       └────────┬───────┘
                │
       ┌────────▼───────┐     ┌────────────┐
       │   PostgreSQL   │────▶│  Fleetio   │
       └────────────────┘     └────────────┘
```

**Bounded contexts**
- **Work orders:** lifecycle, locations, services, supervisors
- **Tasks:** daily assignment, status, ETA, overdue reasons
- **Resources:** staff, fleet/assets, client locations
- **Reporting:** ops KPIs and client-facing progress views

**Role on this project:** architecture and delivery of the NestJS GraphQL API, admin and client portals, fleet wiring, and KPI reporting workstreams.

## Note

This repo is a README showcase. Client application source stays private.
