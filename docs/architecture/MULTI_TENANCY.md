# BuildOS Multi-Tenancy Architecture

## 1. Purpose

BuildOS is a multi-tenant SaaS platform.

Multiple construction companies must be able to use the same
BuildOS application while their users, projects, reports,
documents, site updates, and other resources remain isolated.

A user from one organization must never be able to access
resources belonging to another organization unless an explicit
cross-organization relationship is supported by the system.

---

## 2. Tenant Definition

In BuildOS, a tenant represents a construction organization
using the platform.

Example:

```text
BuildOS
│
├── L&T
├── Tata Projects
└── ABC Infra
```
