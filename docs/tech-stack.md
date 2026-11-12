# Tech stack

## Backend

| Tool | Role |
|---|---|
| **PHP 8.5** | Language |
| **Laravel 13** | Application framework |
| **Laravel Fortify** | Authentication (login, registration, 2FA, password reset) |
| **Laravel Sanctum** | Token auth for the mobile API |
| **Spatie Laravel Permission** | Roles & permissions |
| **maatwebsite/excel** | Excel import/export |
| **mPDF** | PDF document generation |
| **Ziggy** | Laravel named routes in JavaScript |

## Frontend

| Tool | Role |
|---|---|
| **Vue 3** | UI framework |
| **Inertia.js 3** | The glue between Laravel and Vue (no separate web API) |
| **Tailwind CSS** | Styling |
| **TypeScript** | Type-safe front-end code |
| **Vite** | Build tooling & dev server |

## Quality & tooling

| Tool | Role |
|---|---|
| **Pest 4** | Testing framework |
| **Laravel Pint** | Opinionated code-style fixer |
| **ESLint + Prettier** | JS/TS linting & formatting |
| **Laravel Pail** | Live log tailing in development |

## In-house packages

These first-party packages were built for Rabixx ERP and released as open source:

| Package | Purpose |
|---|---|
| [**laravel-ddd-generator**](https://github.com/rabnawazak1/laravel-ddd-generator) | Scaffolds the DDD module structure used throughout the app |
| [**laravel-custom-softdelete**](https://github.com/rabnawazak1/laravel-custom-softdelete) | Audit-friendly soft deletes (`is_deleted`, `deleted_at`, `deleted_by`) |

## Why this stack?

- **Inertia** keeps the project a single Laravel app while still delivering a modern SPA feel — no duplicated API contracts for the web UI.
- **Sanctum** adds a clean, stateless token layer exactly where it's needed: the mobile app.
- **DDD modules** mean a new business area can be added without touching existing ones.
- **Pest + Pint** keep the codebase tested and consistently formatted.
