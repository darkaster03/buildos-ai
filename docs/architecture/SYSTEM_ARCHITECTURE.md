# BuildOS System Architecture

## 1. Purpose

BuildOS is a multi-tenant SaaS platform for construction project
operations.

The system captures field information such as photos, voice notes,
observations, and progress updates, then converts this information
into structured project data, reports, approvals, and project
intelligence.

The architecture is designed around:

- Security
- Multi-tenancy
- Reliability
- Offline-first field operations
- Asynchronous AI processing
- Auditability
- Scalability
- Maintainability

---

## 2. Architecture Principles

BuildOS follows these principles:

### 2.1 Backend is the source of truth

The frontend is considered untrusted.

All important authorization and business rules are enforced on
the backend.

### 2.2 Tenant isolation by design

Every organization using BuildOS operates inside an isolated
tenant context.

Users must never be able to access resources belonging to
another organization.

### 2.3 Modular architecture

BuildOS will initially use a modular monolith rather than
multiple microservices.

Business domains will remain separated through clear module
boundaries so individual components can be extracted later if
required.

### 2.4 Asynchronous processing

Long-running operations such as AI analysis, speech processing,
notifications, and large file processing will be handled
asynchronously through background jobs.

### 2.5 Offline-first field operations

Site engineers must be able to capture essential site information
without a continuous internet connection.

Local data will be synchronized with the backend when connectivity
returns.

### 2.6 Human verification for AI

AI-generated information is advisory.

Important construction decisions and approvals remain under
human control.

---

## 3. High-Level Architecture

```text
                    BUILDOS
                       |
          +------------+------------+
          |                         |
      Web Client              Field Client
      Next.js/PWA             Next.js/PWA
          |                         |
          +------------+------------+
                       |
                      HTTPS
                       |
                       v
                BuildOS API
                  NestJS
                       |
       +---------------+---------------+
       |               |               |
    Identity        Projects        Workflow
    & Auth          & Sites         & Reports
       |               |               |
       +---------------+---------------+
                       |
                       v
                  PostgreSQL
                       |
          +------------+------------+
          |            |            |
        Redis      Object Store    Queue
                     / S3
                       |
                       v
                   AI Workers
                +------+------+
                |      |      |
             Vision  Speech   LLM

```
