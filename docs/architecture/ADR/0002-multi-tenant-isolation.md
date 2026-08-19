# ADR-0002: Use Pooled Multi-Tenancy with Tenant-Scoped Access

## Status

Accepted

## Date

2026-08-19

## Context

BuildOS is intended to serve multiple construction companies from
a single SaaS application.

Each organization must have isolated users, projects, reports,
site updates, files, workflows, and other business resources.

The system must support growth from a small number of customers
to potentially thousands of organizations without requiring a
separate application deployment for every customer.

## Decision

BuildOS will initially use a pooled multi-tenant architecture.

Multiple organizations will share the same PostgreSQL database.

Organization-owned resources will contain an `organization_id`
that identifies their tenant.

Access will be enforced through:

1. Authentication
2. Organization membership
3. Role and permissions
4. Project membership
5. Resource-level authorization
6. Tenant-scoped data access

The frontend will not be considered a security boundary.

## Why

A pooled architecture provides:

- Lower infrastructure cost
- Simpler operations
- Easier deployment
- Efficient resource utilization
- Straightforward scaling for the initial product

It also allows one BuildOS application to serve many organizations.

## Alternatives Considered

### Database per organization

Provides stronger physical isolation but introduces significant
operational complexity as the number of tenants grows.

Rejected for the initial architecture.

### Schema per organization

Provides stronger database-level separation but creates additional
schema management and migration complexity.

Rejected for the initial architecture.

### Pooled multi-tenancy

Selected because it provides a good balance between scalability,
operational simplicity, and cost.

## Security Requirements

Tenant isolation must be enforced server-side.

The application must prevent:

- Cross-tenant resource access
- Unauthorized project access
- Privilege escalation
- IDOR-style resource access
- Cross-tenant cache leakage
- Cross-tenant object-storage access
- Cross-tenant background-job processing

## Consequences

### Positive

- One application can serve many organizations
- Lower infrastructure cost
- Easier deployments
- Easier centralized updates
- Efficient infrastructure utilization

### Negative

- Tenant isolation becomes a critical application responsibility
- Bugs in authorization could have cross-tenant impact
- Strong automated authorization testing is required

## Future Evolution

As BuildOS grows, individual enterprise customers may require
stronger isolation.

The architecture may evolve toward a hybrid model where some
customers use pooled infrastructure while others receive
dedicated databases or infrastructure.

Such changes should be driven by actual business, security,
regulatory, or scalability requirements.
