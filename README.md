# SmoothGig

> **Status: in development.** SmoothGig is not yet released.

SmoothGig is a CRM for small businesses and solo gig workers, such as photographers, wedding vendors, and bakers, who book jobs with clients. It gives the business owner one place to run each job from first inquiry to final payment, and gives each client a simple portal for the job they booked.

## Features

**Vendor dashboard**
- Inquiry tracking for new leads
- Quotes with line items, discounts, and reusable quote packages
- Quote acceptance with contract e-signature
- Projects with client-visible milestones and status
- Client invites (clients get their own login, scoped to their project)
- Contracts (PDF upload and client acknowledgement) and invoices
- Payment settings, including Stripe payment links
- Vendor calendar
- In-app notifications, delivered in real time over Socket.IO
- Business profile and portal branding (name, logo, colors)
- Guided onboarding

**Client portal**
- One login per client, with access only to their own project
- Project status and timeline
- Review and sign contracts, review quotes, view invoices

**Admin**
- Admin dashboard, user management, and settings

## Tech stack

| Layer | Technology |
|-------|------------|
| Front end | React, TypeScript, Vite, Tailwind CSS, React Router, React Query, Zustand |
| Back end | Node.js, Express, TypeScript |
| Database | PostgreSQL (`pg`, sessions via `connect-pg-simple`) |
| Auth | JWT and server sessions, with role-based access (vendor, client, admin) |
| Payments | Stripe |
| Real time | Socket.IO |
| Other | Nodemailer (email), Multer and Sharp (uploads), PDFKit, Helmet, express-rate-limit |
| Testing | Jest (server), Vitest (client) |
| Deployment | Nixpacks (`nixpacks.toml`) |

## Project structure

```
client/     React front end (Vite)
server/     Express API (TypeScript)
database/   Numbered PostgreSQL migrations, plus dev reset and seed scripts
docs/       Beta tester and user acceptance testing guides
```

## Local development

Requirements: Node.js 20 and PostgreSQL.

1. Install dependencies:
   ```bash
   npm run install-all
   ```
2. Copy `.env.example` to `.env` (and `client/.env.example` to `client/.env`), then fill in your own database settings and a unique `JWT_SECRET`.
3. Create the database schema by running the SQL files in `database/` in numeric order. See [`database/README.md`](database/README.md).
4. Start the client and server together:
   ```bash
   npm run dev
   ```

The API runs on port 3000 by default, and the Vite dev server on port 5173.

## Scripts

| Command | What it does |
|---------|--------------|
| `npm run dev` | Runs the client and server together |
| `npm run build` | Builds the client and server |
| `npm start` | Starts the built server |
| `npm run lint` | Lints the server and client |
| `npm run type-check` | Type-checks the server and client |
