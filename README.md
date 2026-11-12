<h1 align="center">Rabixx ERP</h1>

<p align="center">
  A modular, <b>domain-driven</b> ERP for small and mid-sized businesses — Sales, Purchasing, Inventory,
  double-entry Ledger, and CRM in one Laravel application.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Laravel-13-FF2D20?style=flat-square&logo=laravel&logoColor=white" alt="Laravel 13"/>
  <img src="https://img.shields.io/badge/PHP-8.5-777BB4?style=flat-square&logo=php&logoColor=white" alt="PHP 8.5"/>
  <img src="https://img.shields.io/badge/Vue-3-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white" alt="Vue 3"/>
  <img src="https://img.shields.io/badge/Inertia.js-3-9553E9?style=flat-square&logo=inertia&logoColor=white" alt="Inertia 3"/>
  <img src="https://img.shields.io/badge/Tests-Pest_4-5f67ea?style=flat-square" alt="Pest"/>
  <img src="https://img.shields.io/badge/status-in%20active%20development-blue?style=flat-square" alt="Status"/>
</p>

> **About this repository**
> This is a public **showcase** of Rabixx ERP — it documents the architecture and feature set of the project.
> The application source code lives in a private repository and is **not** published here.

---

## What is Rabixx ERP?

Rabixx ERP is a full-stack business management system. Instead of a tangle of controllers and models, it is organised into **self-contained domain modules** that each own their models, routes, policies, and business logic. Domains never reach into each other directly — they communicate through **domain events**, which keeps the system easy to reason about as it grows.

The front end is a single-page experience built with **Vue 3 + Inertia.js**, served straight from Laravel with no separate API to maintain for the web app. A dedicated **Sanctum-secured mobile API** powers the companion [RabixxCRM Flutter app](https://github.com/rabnawazak1/rabixx-crm).

## Highlights

- 🧱 **Domain-Driven Design** — seven independent business domains, each in its own module
- 📡 **Event-driven core** — cross-domain communication only through events, never direct imports
- 🛒 **End-to-end sales flow** — quotation → sales order → invoice → goods issue, plus a POS and Food POS
- 📦 **Purchasing & inventory** — purchase orders, goods receipt, and serial-number tracking
- 📒 **Double-entry ledger** — chart of accounts, journal/payment/receipt/contra vouchers, trial balance
- 🤝 **Built-in CRM** — leads, pipelines, deals, activities, and follow-ups
- 🔐 **Role-based access** — Fortify authentication with Spatie roles & permissions and dynamic menus
- 📱 **Mobile-ready** — a versioned `api/v1` layer secured with Laravel Sanctum
- 🧾 **Documents** — Excel exports and PDF generation out of the box

## Explore the docs

| Document | What's inside |
|---|---|
| [**Modules**](docs/modules.md) | Every business domain and the entities it manages |
| [**Architecture**](docs/architecture.md) | How the domains, events, and layers fit together |
| [**Tech stack**](docs/tech-stack.md) | The frameworks, libraries, and tooling behind it |

## At a glance

| | |
|---|---|
| **Backend** | Laravel 13 (PHP 8.5) |
| **Frontend** | Vue 3 + Inertia.js + Tailwind CSS |
| **Auth** | Laravel Fortify + Sanctum + Spatie Permission |
| **Testing** | Pest 4 |
| **Domains** | Access · CRM · Sales · Purchasing · Inventory · Ledger · Misc |

---

<p align="center"><sub>Part of the Rabixx platform — see also <a href="https://github.com/rabnawazak1/rabixx-crm">RabixxCRM</a>.</sub></p>
