# ADR-0001: Use a Modular Monolith for the Initial BuildOS Backend

## Status

Accepted

## Date

2026-08-19

## Context

BuildOS is an early-stage multi-tenant SaaS platform for
construction project operations.

The system will contain multiple business domains including:

- Identity
- Organizations
- Authorization
- Projects
- Site Updates
- Reports
- Approvals
- Audit

The system is expected to scale significantly in the future, but
the initial engineering team and product scope do not justify the
operational complexity of a microservices architecture.

## Decision

BuildOS will initially use a modular monolith architecture.

The backend will be deployed as a single application while
maintaining strict logical boundaries between business domains.

Each domain will have its own module, responsibilities, services,
and business logic.

The initial structure will conceptually follow:

```text
BuildOS API
│
├── Identity
├── Organizations
├── Authorization
├── Projects
├── Sites
├── Site Updates
├── Reports
├── Approvals
└── Audit
```
