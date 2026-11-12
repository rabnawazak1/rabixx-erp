# Architecture

Rabixx ERP follows a pragmatic take on **Domain-Driven Design (DDD)** on top of Laravel. The goal is simple: keep each business area self-contained so the system stays understandable as it grows.

## Domain modules

Every business area is a module under `app/Domains/<Domain>/` with a consistent shape:

```
app/Domains/<Domain>/
├── Actions/        # single-responsibility use-case classes
├── Events/         # domain events (the only cross-domain channel)
├── Http/
│   ├── Controllers/
│   ├── Requests/
│   └── Resources/  # API / Inertia resources
├── Models/         # Eloquent models for this domain
├── Policies/       # authorization policies
├── Services/       # orchestration (no HTTP context)
└── routes.php      # auto-loaded routes
```

The modules themselves are scaffolded with a custom Artisan generator,
[**laravel-ddd-generator**](https://github.com/rabnawazak1/laravel-ddd-generator).

## The one rule: no direct cross-domain imports

Domains do **not** reach into each other. When something in one domain needs to react to something in another, it listens for a **domain event** instead.

| Scenario | Allowed? |
|---|---|
| `Sales` imports from `Sales` | ✅ |
| `Sales` fires an event, `Ledger` listens to it | ✅ |
| `Sales` imports a model from `Inventory` | ❌ |
| `Sales` calls a `CRM` service directly | ❌ |
| Any domain imports from `app/Shared/` | ✅ |

**Rule of thumb:** if you're typing `App\Domains\<A>\…` inside a file that belongs to `App\Domains\<B>`, stop and introduce an event instead. This keeps domains swappable and their boundaries honest.

## Request lifecycle

A typical write request flows through clear layers:

```
Request → Controller → Service → Action → Model
              │            │         │
          FormRequest   orchestrates  does one thing
          (validation)   the workflow  in a DB transaction
```

- **Controllers** stay thin — they validate (via Form Requests) and delegate.
- **Services** orchestrate a workflow across one or more actions.
- **Actions** each do a single job, usually inside a database transaction.
- **Events** announce that something happened, letting other domains react.

## Auto-loaded routes

Each domain ships its own `routes.php`, discovered automatically at boot:

```php
foreach (glob(base_path('app/Domains/*/routes.php')) as $routeFile) {
    Route::middleware('web')->group($routeFile);
}
```

Each file manages its own middleware and naming convention (`sales.*`, `ledger.*`, and so on). Adding a domain is as simple as creating its folder and dropping in a `routes.php`.

## Web and mobile, one backend

- **Web** — Vue 3 pages rendered through **Inertia.js**, so there's no separate API to maintain for the browser app. [Ziggy](https://github.com/tighten/ziggy) exposes named routes to the front end.
- **Mobile** — a versioned `api/v1` layer secured with **Laravel Sanctum** personal-access tokens, consumed by the [RabixxCRM Flutter app](https://github.com/rabnawazak1/rabixx-crm).

## Data integrity

- **Custom soft deletes** via [laravel-custom-softdelete](https://github.com/rabnawazak1/laravel-custom-softdelete) record *who* deleted a row and *when* (`is_deleted`, `deleted_at`, `deleted_by`).
- **Document counters** generate gap-free sequential numbers for invoices, orders, and vouchers.
- The **Ledger** enforces double-entry balancing across every posting.
