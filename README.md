
[![Documented with Setinstone.io](https://img.shields.io/badge/⛰️Documented%20with-Setinstone.io-success?logo=book&logoColor=white)](https://calendly.com/set-in-stone-thomas-benoit/setinstone-demo)
![License](https://img.shields.io/github/license/thomgit9/monorepo)
![Last Commit](https://img.shields.io/github/last-commit/thomgit9/monorepo/main)
![Contributors](https://img.shields.io/github/contributors/thomgit9/monorepo)

# Monorepo

## Presentation

This repository — [**thomgit9/monorepo**](https://github.com/thomgit9/monorepo) — hosts **all Devcon and Devconnect-related applications and infrastructure** for the Ethereum Foundation.

It brings together the official websites, APIs, archives, and shared libraries used across projects that support the Ethereum community’s major events:

- [**Devcon**](https://devcon.org/) – Ethereum’s global conference for developers, thinkers, and creators  
- [**Devconnect**](https://devconnect.org/) – A week-long collection of community-organised mini-events to foster collaboration and knowledge sharing

### Projects

| Project | Path | Description | Link |
|----------|------|--------------|------|
| **archive** | [/archive](/archive/README.md) | Devcon video archive | [archive.devcon.org](https://archive.devcon.org/) |
| **devcon** | [/devcon](/devcon/README.md) | Main Devcon website | [devcon.org](https://devcon.org/) |
| **devcon-api** | [/devcon-api](/devcon-api/README.md) | API powering Devcon-related apps | [api.devcon.org](https://api.devcon.org/) |
| **devcon-app** | [/devcon-app](/devcon-app/README.md) | Devcon schedule and companion app | [app.devcon.org](https://app.devcon.org/) |
| **devconnect** | [/devconnect](/devconnect/README.md) | Main Devconnect site | [devconnect.org](https://devconnect.org/) |
| **data** | [/devcon-api/data](/devcon-api/data) | JSON data including sessions, speakers, and events | — |
| **lib** | [/lib](/lib/README.md) | Shared components and logic reused by all projects | — |

---

## Prerequisite

- **Node.js** `>= 18`
- **pnpm** package manager (check the `packageManager` key in `package.json` for the correct version)
- **PostgreSQL** (for API session storage)
- **Netlify CLI** *(optional, for local deployments)*

---

## Installation

Install all packages from the root folder using **pnpm**:

```bash
pnpm install
```

To install dependencies for a specific app only (e.g. `devconnect-app`):

```bash
pnpm install --filter devconnect-app
```

> ⚠️ Do **not** commit non-pnpm lockfiles.  
> This can break the deployment process (especially Netlify).  
> pnpm strictly enforces explicit dependencies — phantom (undeclared) imports will fail until properly added.

---

## Configurations

Each service reads configuration values from environment variables (**.env** or deployment settings):

| Variable | Default | Description |
|-----------|----------|-------------|
| `SERVER_CONFIG.PORT` | `3000` | Port used by the API in development |
| `SERVER_CONFIG.NODE_ENV` | `development` | Environment mode (`production`, `staging`, `development`) |
| `SESSION_CONFIG.cookieName` | — | Session identifier name |
| `SESSION_CONFIG.password` | — | Session encryption secret |
| `DATABASE_URL` | — | Connection string for PostgreSQL (session + API data) |
| `ALLOWED_ORIGINS` | predefined list | Whitelisted CORS origins for API access |
| `NEXT_PUBLIC_API_URL` | `https://api.devcon.org` | Client-side API endpoint for Next.js apps |
| `NETLIFY_SITE_ID` | — | Used internally for CI/CD builds |
| `NODE_OPTIONS` | — | Custom Node.js runtime flags (optional) |

---

## Usage

**Development**

To start any project’s local server:

```bash
cd <project-folder>
pnpm run dev
```

Examples:

```bash
cd devcon-api
pnpm run dev
```

or

```bash
cd devconnect
pnpm run dev
```

Open in your browser:
- `http://localhost:3000` – for frontend apps
- `http://localhost:4000` – for API (if configured as such)

**Production build**

```bash
pnpm run build
```

Then run services through the corresponding launch scripts or CI/CD pipelines (GitHub Actions / Netlify).

---

## Functions and Classes principales

| Name | File | Description | Inputs | Outputs |
|------|------|-------------|---------|----------|
| `app` | `devcon-api/src/app.ts` | Configures and initializes the Express server with middlewares (CORS, sessions, swagger, static routes). | `Request`, `Response`, `NextFunction` | `Express.Application` |
| `router` | `devcon-api/src/routes/index.ts` | Aggregates API route definitions for Devcon API. | HTTP routes | Express Router |
| `main` | `devcon-api/src/services/at-slurper/main.ts` | Synchronizes external event data (AT Protocol, Pretix) with Notion-managed event pages. | External API data | Upserted Notion events |
| `appState` | `devcon/src/state/main.ts` | Recoil atom maintaining global UI visibility state (`devabotVisible`). | — | Recoil atom |
| `workbox` service worker | `devcon-app/workbox/index.js` | Handles push notifications and user actions for the Devcon App. | Push message payload | Web Notification displayed |
| `express-session` configuration | `devcon-api/src/app.ts` | Defines cookie session behavior and database-backed persistence. | `SESSION_CONFIG`, `pgSessionStore` | Registered middleware for express |
| `SERVER_CONFIG` | `devcon-api/src/utils/config.ts` | Centralizes environment configuration readout for server startup. | `.env` variables | Configuration constants |
| `index.ts` | `devcon-api/src/index.ts` | Starts the Express app and logs environment info. | — | Running HTTP server instance |

---

## ⛰️ Documented With SetinStone.io

Focus on the only task that matters: **building your codebase!**  
With every developer push, Set In Stone’s Mirror Documentation Agent updates your `README.md` via a pull request — ready for you to review, edit, and approve.

[Book a demo](https://calendly.com/set-in-stone-thomas-benoit/setinstone-demo)
```
