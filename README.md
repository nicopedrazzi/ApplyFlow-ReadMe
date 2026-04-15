<h1 align="center">ApplyFlow</h1>

<p align="center">
  A job search tracker built to make the process feel calmer, clearer, and more controlled.
</p>

<p align="center">
  ApplyFlow helps you save job board sources or company websites, bookmark roles for later, move opportunities into your pipeline, and keep notes on every application without losing momentum.
</p>

<p align="center">
  <a href="#screenshots">Screenshots</a>
  ·
  <a href="#features">Features</a>
  ·
  <a href="#tech-stack">Tech Stack</a>
  ·
  <a href="#getting-started">Getting Started</a>
  ·
  <a href="#deployment">Deployment</a>
</p>

<p align="center">
  <img alt="Next.js 16" src="https://img.shields.io/badge/Next.js-16-black?logo=nextdotjs" />
  <img alt="React 19" src="https://img.shields.io/badge/React-19-149eca?logo=react&logoColor=white" />
  <img alt="Express 5" src="https://img.shields.io/badge/Express-5-222222?logo=express&logoColor=white" />
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-16-336791?logo=postgresql&logoColor=white" />
  <img alt="Drizzle ORM" src="https://img.shields.io/badge/Drizzle-ORM-c5f74f" />
  <img alt="Better Auth" src="https://img.shields.io/badge/Auth-Better%20Auth-111111" />
  <img alt="Vercel" src="https://img.shields.io/badge/Deploy-Vercel-black?logo=vercel" />
  <img alt="GitHub Actions" src="https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088ff?logo=githubactions&logoColor=white" />
</p>

## Overview

Job hunting can get messy fast. Links end up everywhere, interesting roles get forgotten, and application status tracking becomes a spreadsheet problem before long.

ApplyFlow is a focused job search companion that brings those moving parts into one flow:

- save companies and job boards you want to revisit
- store roles you are interested in
- move saved roles into active applications with one click
- track application status and notes over time
- keep momentum with simple weekly progress stats

The product direction is intentionally lightweight: fewer tabs, fewer decisions, and more visible progress.

## Features

- Secure authentication with email/password
- Dedicated job source tracking for companies and job boards
- Favourite lead sources for quick access during search sessions
- Saved-for-later workflow for roles you are not ready to apply to yet
- One-click conversion from saved role to active application
- Application pipeline management with editable statuses
- Notes per application for prep, follow-ups, and reminders
- Weekly dashboard stats to surface momentum

## Screenshots

| Screen | What To Show |
| --- | --- |
| Landing / Auth |  |
| Dashboard |  |
| Search Job |  |
| Saved For Later |  |
| Applications |  |

## Tech Stack

| Layer | Tools |
| --- | --- |
| Frontend | Next.js 16, React 19, TypeScript, Tailwind CSS 4 |
| Backend | Express 5, TypeScript |
| Database | PostgreSQL |
| ORM / Migrations | Drizzle ORM, Drizzle Kit |
| Auth | Better Auth with email/password and optional Google/GitHub providers |
| Infra | Vercel, GitHub Actions, Docker Compose |
| Monorepo | npm workspaces |

## Project Structure

```text
applyflow/
├── apps/
│   ├── api/        # Express API, auth, database, migrations
│   └── web/        # Next.js frontend
├── packages/
│   └── contracts/  # Shared package space for cross-app contracts
├── .github/
│   └── workflows/  # CI and production deployment pipelines
├── compose.yaml
└── package.json
```

## How It Works

### 1. Search smarter

Users can save lead sources such as company career pages or job boards, and mark favourites for quick repeat visits.

### 2. Save roles without losing them

Interesting roles can be added to a saved list instead of being forgotten in browser tabs.

### 3. Move from intent to action

When it is time to apply, a saved role can be moved into the application pipeline in one step.

### 4. Track the process

Applications can be updated with statuses like `sent`, `interview`, `offer`, and `rejected`, plus freeform notes.

### 5. Keep momentum visible

The dashboard summarizes weekly activity so progress feels tangible, even in a long search cycle.

## Getting Started

### Prerequisites

- Node.js 22+
- npm
- Docker Desktop or a local PostgreSQL instance

### 1. Clone and install

```bash
git clone <your-repo-url>
cd applyflow
npm ci
```

### 2. Create your environment file

```bash
cp .env.example .env
```

The local defaults expect:

- web app on `http://localhost:3000`
- API on `http://localhost:3001`
- PostgreSQL on `localhost:5432`

### 3. Start the database

If you want the fastest local setup, start Postgres with Docker:

```bash
docker compose up db -d
```

### 4. Run the apps

```bash
npm run dev
```

This starts:

- the Next.js app in `apps/web`
- the Express API in `apps/api`

Local API development runs Drizzle migrations automatically before booting the server.

## Docker Setup

To run the whole stack with containers:

```bash
docker compose up --build
```

This brings up:

- PostgreSQL
- the Express API
- the Next.js frontend

## Environment Variables

Core local variables from `.env.example`:

| Variable | Purpose |
| --- | --- |
| `PORT` | API port |
| `WEB_URL` | Base URL of the web app |
| `BETTER_AUTH_URL` | Better Auth callback base |
| `BETTER_AUTH_SECRET` | Auth secret, should be 32+ chars in production |
| `DATABASE_URL` | PostgreSQL connection string |
| `POSTGRES_DB` | Local database name |
| `POSTGRES_USER` | Local database user |
| `POSTGRES_PASSWORD` | Local database password |
| `GOOGLE_CLIENT_ID` | Optional Google OAuth |
| `GOOGLE_CLIENT_SECRET` | Optional Google OAuth |
| `GITHUB_CLIENT_ID` | Optional GitHub OAuth |
| `GITHUB_CLIENT_SECRET` | Optional GitHub OAuth |

For Vercel deployments, the web app also expects:

| Variable | Purpose |
| --- | --- |
| `API_INTERNAL_URL` | Internal API origin for Vercel builds |
| `NEXT_PUBLIC_API_URL` | Public API base URL when needed |

## Scripts

| Command | What It Does |
| --- | --- |
| `npm run dev` | Runs the API and web app together |
| `npm run build` | Builds all workspaces |
| `npm test` | Runs the API test suite used by CI |
| `npm run typecheck` | Type-checks all workspaces |
| `npm run db:migrate -w @applyflow/api` | Runs Drizzle migrations |
| `npm run db:generate -w @applyflow/api` | Generates new migrations |

## Deployment

ApplyFlow is deployed with a GitHub Actions + Vercel workflow:

- CI runs on push, pull request, and manual dispatch
- production deploy runs on `main`
- database migrations execute before deployment
- the API and web app are deployed as separate Vercel projects
- Vercel handles the production build, while GitHub Actions coordinates the release flow

This setup reduces the risk of shipping new code against an old database schema.

## Why This Project Is Interesting

ApplyFlow is more than a CRUD app. It pulls together several concerns that often break in real projects:

- multi-app monorepo structure
- authenticated user-specific data flows
- database schema evolution with migrations
- UX details that encourage repeated use
- CI/CD coordination across web, API, and database layers

It is a strong example of building a product with both user empathy and production discipline.

## Possible Next Steps

- richer analytics for application outcomes
- reminders or follow-up prompts
- tagging and filtering for applications
- interview timeline view
- export / import support
- shared opportunities board or collaboration features

## Author Notes

This README is written to showcase the project in a portfolio-style GitHub context. If you plan to move it to a separate repository, you can easily add:

- live demo links
- architecture diagrams
- GIF walkthroughs
- screenshots in the placeholders above
- a short "What I learned" section in your own voice
