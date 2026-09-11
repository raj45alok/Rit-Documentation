# Rit --- Technical Architecture

**Phase 1:** Web-only\
**Architecture:** Modular monolith

## 1. Final stack

### Frontend

-   Next.js
-   React
-   TypeScript
-   Tailwind CSS
-   IndexedDB
-   Playwright

### Backend

-   Python
-   FastAPI
-   Pydantic
-   SQLAlchemy 2.x
-   Alembic
-   pytest

### Database

-   PostgreSQL

Use managed infrastructure initially; keep the application
container-portable.

## 2. System context

``` text
Browser
 ├─ Next.js UI
 ├─ IndexedDB
 └─ Sync queue
       │ HTTPS
       ▼
FastAPI modular monolith
 ├─ Auth
 ├─ Identity
 ├─ Users/Guardians/Assessors
 ├─ Institutions
 ├─ Data Subjects
 ├─ Consent/Authorization
 ├─ Eligibility
 ├─ Assessments
 ├─ Activities
 ├─ Reports
 ├─ Incidents
 ├─ Sync
 └─ Audit
       │
       ▼
PostgreSQL
```

Optional later: object storage, worker queue, Redis, external
notification/identity providers.

## 3. Backend modules

``` text
app/
  auth/
  identity/
  users/
  guardians/
  assessors/
  institutions/
  subjects/
  consent/
  assessments/
  eligibility/
  activities/
  reports/
  incidents/
  audit/
  sync/
  common/
```

Modules interact through use cases/service interfaces rather than direct
cross-domain SQL.

## 4. Authentication

Phone + OTP initially. Short-lived access token plus refresh session.
Rate-limit OTP send/verify. Support device/session revocation.

## 5. Authorization

Every protected request performs server-side role and relationship
checks.

Example:

``` text
Assessor X
 + member of Institution A
 + active authorization for Subject Y in A
 = allowed
```

Otherwise deny without exposing unnecessary resource existence.

## 6. Consent

Separate mutable authorization state from immutable consent events.
Store policy/version/hash where appropriate. Do not make DigiLocker
legally mandatory without explicit verification.

## 7. Assessment engine

Definitions are immutable and versioned. Historical assessments point to
exact battery/test/normative versions.

## 8. State machine

``` text
DRAFT → SUBMITTED → REVIEWED → FINALIZED
```

Domain services enforce valid transitions. Optimistic concurrency
protects against simultaneous edits.

## 9. Offline web architecture

IndexedDB stores the minimum data needed for active assessment
workflows: - authorized roster; - assessment definitions; - current
assessment; - immutable local revisions; - sync queue; - conflict
metadata.

Treat browser storage as sensitive. Clear/expire data when authorization
ends and avoid unsafe token storage.

## 10. Sync protocol

Every mutation includes: - client_revision_id; - parent_revision_id; -
device_id; - entity/version context.

Server checks authentication, authorization, idempotency, parent
revision, state, schema/version and conflicts.

Never use last-write-wins.

## 11. API

REST/JSON under `/v1`.

Examples: - POST `/v1/auth/otp` - POST `/v1/auth/verify` - POST
`/v1/sync` - POST `/v1/assessment-sessions` - POST
`/v1/assessments/{id}/submit` - POST `/v1/assessments/{id}/review` -
POST `/v1/assessments/{id}/finalize` - GET
`/v1/data-subjects/{id}/reports` - POST `/v1/incidents` - POST
`/v1/data-subjects/{id}/erasure-request`

Use idempotency keys for retry-sensitive mutations.

## 12. Integrity

Use PostgreSQL foreign keys, unique/check constraints, transactions and
immutable/versioned definitions. Put cross-table business rules in
domain services rather than unrealistic CHECK constraints.

## 13. Privacy/deletion

Controlled deletion workflow: request → authorization → deletion job →
personal-data cleanup → storage/cache cleanup → verification → minimal
audit.

Do not call a k-threshold a legal anonymization guarantee.

## 14. Object storage

Only store artifacts that have a justified product need. Private
buckets, encryption, short-lived access, access auditing and lifecycle
policies. Avoid unnecessary identity-document retention.

## 15. Security

HTTPS, secure session handling, strict CORS, CSRF protection where
applicable, input validation, parameterized SQL, secrets management,
vulnerability scanning, secure headers and authorization/IDOR tests.

## 16. Background jobs

Do not introduce Redis/queues until real asynchronous workloads justify
them. Use the simplest reliable mechanism first.

## 17. Observability

Structured logs/metrics/traces without child PII. Track latency,
4xx/5xx, auth abuse, sync throughput/failure/conflict, assessment
lifecycle and deletion failures.

## 18. Testing

Unit: eligibility, scoring, state transitions, authorization, conflict
detection.

Integration: PostgreSQL, transactions, consent, authorization, deletion.

E2E: onboarding, guardian consent, assessment, offline/online,
conflicts, reports.

Security: IDOR, cross-institution access, session revocation, rate
limiting and data leakage.

## 19. CI/CD

GitHub Actions for linting, formatting, type checks, tests, integration
tests, E2E, dependency scanning and migration checks.

Use expand/contract patterns for risky schema changes.

## 20. Deployment

Start:

``` text
Managed Next.js hosting
        ↓
FastAPI container
        ↓
Managed PostgreSQL
```

Add load balancing, Redis, workers and autoscaling only when justified.

## 21. Backup/recovery

Use managed backups/PITR where available. Define and test RPO/RTO
instead of asserting untested numbers.

## 22. ADRs

-   ADR-001 Web-only Phase 1
-   ADR-002 Next.js + TypeScript
-   ADR-003 FastAPI + Python
-   ADR-004 PostgreSQL
-   ADR-005 Modular monolith
-   ADR-006 IndexedDB offline storage
-   ADR-007 Append-only assessment revisions
-   ADR-008 Explicit conflict resolution/no LWW
-   ADR-009 Identity provider abstraction
-   ADR-010 Server-side authorization
-   ADR-011 No microservices in Phase 1
-   ADR-012 No premature Redis/queue

## 23. Final architecture

``` text
Next.js + TypeScript
        │
       HTTPS
        │
FastAPI + Python
        │
   PostgreSQL
```

This is the Phase 1 engineering baseline.
