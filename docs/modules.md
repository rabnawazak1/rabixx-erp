# Modules

Rabixx ERP is divided into **seven domain modules**. Each one lives in its own folder and owns its models, controllers, routes, policies, and services. Below is what each domain manages.

---

## 🔐 Access

Authentication, authorisation, and the application shell.

- **Users** — accounts, profiles, and device tokens for push notifications
- **Roles & Permissions** — fine-grained, role-based access control
- **Menus** — dynamic, permission-aware navigation
- **Settings** — per-user and application-level preferences

*Key entities:* `User`, `Menu`, `DeviceToken`

---

## 🤝 CRM

The customer-relationship side of the business, also exposed over the mobile API.

- **Leads** — captured prospects with sources and status tracking
- **Pipelines & Stages** — configurable sales pipelines (kanban-style stages)
- **Deals** — opportunities moving through a pipeline
- **Companies & Contacts** — the people and organisations behind each lead
- **Activities** — calls, meetings, and **follow-ups**
- **Notes & Attachments** — context attached to any record

*Key entities:* `Lead`, `LeadSource`, `Pipeline`, `Stage`, `Deal`, `Company`, `Contact`, `Activity`, `Note`, `CrmAttachment`

---

## 🛒 Sales

The full order-to-delivery flow, plus point of sale.

- **Quotations** → **Sales Orders** → **Sales Invoices** → **Goods Issues**
- **POS** — a fast point-of-sale screen
- **Food POS** — a POS variant tailored to food-service workflows
- **Serial tracking** — serial numbers captured on invoices and goods issues

*Key entities:* `Quotation`, `SalesOrder`, `SalesInvoice`, `GoodsIssue` (each with line items and, where relevant, item serials)

---

## 📦 Purchasing

Procurement and inward stock.

- **Purchase Orders** — raise and track orders to suppliers
- **Receive Orders** — record goods received against a purchase order
- **Serial capture** — serial numbers recorded at receipt

*Key entities:* `PurchaseOrder`, `ReceiveOrder` (with line items and item serials)

---

## 📥 Inventory

Products and stock.

- **Products** — the catalogue, with serial-number support
- **Categories** — product classification
- **Serials** — per-unit serial records for traceability

*Key entities:* `Product`, `ProductSerial`, `Category`

---

## 📒 Ledger

A double-entry accounting engine.

- **Chart of Accounts** — the account tree
- **Vouchers** — Journal, Payment, Receipt, and Contra vouchers
- **Account Ledger** — per-account transaction history
- **Trial Balance** — balance verification across all accounts

*Key entities:* `LedgerVoucher`, `LedgerVoucherLine`

---

## ⚙️ Misc (Master Data)

The shared reference data the other domains build on.

- **Customers & Suppliers** — trading partners
- **Accounts & Sub-Accounts** — financial master data
- **Currencies & Units** — multi-currency amounts and units of measure
- **Counters** — automatic document numbering (invoices, orders, vouchers…)
- **Settings** — global configuration

*Key entities:* `Customer`, `Supplier`, `Account`, `SubAccount`, `Currency`, `Unit`, `Counter`, `Setting`

---

## 🧩 Shared

Cross-cutting building blocks reused by every domain:

- `Attachment` — polymorphic file attachments
- `UsesDocumentCounter` — a trait for sequential document numbers
- `PdfHelper` — PDF generation (mPDF)
- `HasPermissions` — a permission contract
- Reusable validation rules and helpers

> Domains may use `Shared/`, but **never** import from one another directly — see [Architecture](architecture.md).
