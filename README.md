[![Documented with Setinstone.io](https://img.shields.io/badge/⛰️Documented%20with-Setinstone.io-success?logo=book&logoColor=white)](https://calendly.com/set-in-stone-thomas-benoit/setinstone-demo)

# Devcon/nect Monorepo

## Presentation

**Repository:** [thomgit9/monorepo](https://github.com/thomgit9/monorepo)  
**Description:** Main repository for all **Devcon** and **Devconnect**-related applications, managed by the Ethereum Foundation.  
This monorepo centralizes the source code, shared libraries, and APIs powering key community-facing sites and tools:

- **Devcon** — the official Ethereum developer conference ([devcon.org](https://devcon.org))  
- **Devconnect** — a week-long gathering for Ethereum collaboration ([devconnect.org](https://devconnect.org))

It consolidates websites, apps, archives, and APIs to streamline deployment, versioning, and data consistency across all EF event platforms.

---

## Installation

This repository uses **pnpm workspaces** to manage multiple interdependent projects.

1. **Install dependencies for all workspaces:**
   ```bash
   pnpm install
   ```

2. **Install for a specific project only:**
   ```bash
   pnpm install --filter devconnect-app...
   ```

3. **Run a project in development mode:**
   ```bash
   pnpm run dev
   ```

> **Notes:**
> - Ensure your **pnpm version** matches the `packageManager` field in the root `package.json`.
> - Avoid committing non‑pnpm lockfiles (e.g. `package-lock.json` or `yarn.lock`) to prevent build issues with Netlify.
> - pnpm disallows *phantom dependencies*: explicitly install missing peer dependencies if required.

---

## Usage

Each subproject can be started individually:

| Project | Path | Live URL |
|----------|------|----------|
| **Archive** | `/archive` | [archive.devcon.org](https://archive.devcon.org) |
| **Devcon** | `/devcon` | [devcon.org](https://devcon.org) |
| **Devcon API** | `/devcon-api` | [api.devcon.org](https://api.devcon.org) |
| **Devcon App** | `/devcon-app` | [app.devcon.org](https://app.devcon.org) |
| **Devconnect** | `/devconnect` | [devconnect.org](https://devconnect.org) |
| **Shared Library** | `/lib` | internal shared modules |
| **Data** | `/devcon-api/data` | JSON data for sessions, speakers, rooms, and games |

Start the API server:

```bash
cd devcon-api
pnpm start
```

Access local routes:

- `http://localhost:<PORT>/docs` → Swagger UI  
- `http://localhost:<PORT>/data` → public JSON datasets

Run front-end projects using Next.js (e.g., `devcon`, `devconnect`, or `devcon-app`) with:

```bash
pnpm run dev
```

---

## Functions and Classes Principales

| Name | File | Description | Inputs | Outputs |
|------|------|-------------|---------|----------|
| `app` | `devcon-api/src/app.ts` | Configures and instantiates the main Express application. Handles CORS, JSON parsing, sessions, static assets, and Swagger UI. | Express request handlers and middleware | Configured Express app instance |
| `pgSessionStore` | `devcon-api/src/app.ts` | PostgreSQL-backed session store via `connect-pg-simple`. | Database pool and session options | Session persistence layer |
| `sessionConfig` | `devcon-api/src/app.ts` | Defines cookie and session parameters for secure production and development modes. | Environment and server config | SessionOptions object |
| `router` | `devcon-api/src/routes` | API route definitions (imported). | Express Request | JSON API responses |
| `main()` | `devcon-api/src/services/at-slurper/main.ts` | Fetches external events (AT Protocol, Pretix), merges into Notion DB, and updates new or existing records. | External event data and Notion schema | Console logs, updated Notion table rows |
| `appState` | `devcon/src/state/main.ts` | Recoil atomic state controlling the Devabot visibility in Devcon frontend. | Boolean state | Global state atom |
| `push` event listener | `devcon-app/workbox/index.js` | Handles push notifications via Workbox Service Worker and shows `Devcon SEA Passport` messages. | Push event payload | Browser notification UI |
| `notificationclick` handler | `devcon-app/workbox/index.js` | Opens target URLs or focuses an existing client window when notification is clicked. | Click event | Browser window focus/open |
| `index.ts` (server entry) | `devcon-api/src/index.ts` | Starts API HTTP server and logs environment. | PORT, NODE_ENV | Console output & running server |

---

## ⛰️ Documented With SetinStone.io
 Focus on the only task that matters: building your codebase! With every developer push, Set In Stone’s Mirror Documentation Agent updates your README.md via a pull request — ready for you to review, edit, and approve.

[Book a demo](https://calendly.com/set-in-stone-thomas-benoit/setinstone-demo)