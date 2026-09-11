# 08 — Implementation Plan

## 1. Purpose

This document converts the Rit product, data, workflow, and technical decisions into an implementation sequence.

It is an engineering execution plan for Phase 1. It does not redefine the product scope. The PRD, App Flow, Schema, Feature Description, Technical Architecture, and Product Specification remain the primary sources of truth.

---

## 2. Implementation Principles

1. Build the smallest complete vertical workflow before expanding feature breadth.
2. Keep the Phase 1 architecture as a modular monolith.
3. Keep the web-first approach: Next.js + TypeScript frontend and FastAPI + Python backend.
4. Use PostgreSQL as the authoritative server database.
5. Use IndexedDB for browser-side offline assessment capture.
6. Never use silent last-write-wins for assessment data.
7. Treat assessment history and score revisions as append-only/auditable where specified.
8. Keep eligibility and assessment rules explicit and testable.
9. Keep safeguarding, consent, authorization, and auditability in the core implementation rather than adding them later.
10. Keep AI/video analysis out of Phase 1 implementation unless explicitly re-scoped.

---

## 3. Phase 0 — Repository and Development Setup

### Objectives

Create a clean engineering foundation before implementing product features.

### Tasks

- Create the separate Rit application repository.
- Initialize frontend and backend projects.
- Configure TypeScript and Python development environments.
- Configure environment-variable handling.
- Set up PostgreSQL for local development.
- Add SQLAlchemy 2.x and Alembic.
- Establish project linting and formatting.
- Establish test frameworks.
- Add basic CI checks.
- Create development, test, and production configuration boundaries.
- Document local setup.

### Exit Criteria

- Frontend starts locally.
- FastAPI starts locally.
- Backend connects to PostgreSQL.
- Alembic can create and apply migrations.
- CI runs lint/type/test checks.
- No secrets are committed.

---

## 4. Phase 1 — Identity, Roles, and Institution Access

### Objectives

Establish the access-control foundation before handling child assessment data.

### Tasks

- Implement user identity.
- Implement roles required by Phase 1.
- Implement coach/assessor profile.
- Implement institution and institution membership.
- Implement server-side authorization.
- Implement guardian relationships.
- Implement data-subject representation.
- Implement institution authorization boundaries.
- Add audit events for security-sensitive actions.

### Required Security Properties

- A user cannot access another institution's data without explicit authorization.
- Authorization is enforced server-side.
- Child data is not exposed merely because a client knows an ID.
- Sensitive actions produce auditable events.

### Exit Criteria

- Users can authenticate.
- Roles are enforced.
- Institution-level access boundaries work.
- Guardian/data-subject relationships are represented.
- Unauthorized access tests pass.

---

## 5. Phase 2 — Consent and Safeguarding Foundation

### Objectives

Make consent and safeguarding part of the data lifecycle before assessment workflows go live.

### Tasks

- Implement consent-event recording.
- Support guardian consent where required.
- Record consent status and relevant timestamps.
- Implement consent revocation workflow.
- Define restricted actions after revocation.
- Implement incident-report records.
- Implement audit trail for safeguarding-sensitive actions.
- Establish controlled access to child media/data if introduced.
- Avoid direct uncontrolled coach-child communication features.

### Exit Criteria

- Consent can be recorded and audited.
- Revocation is represented without silently deleting historical audit evidence.
- Restricted actions after revocation are enforced.
- Safeguarding incidents have an auditable lifecycle.

---

## 6. Phase 3 — Assessment Configuration and Eligibility Engine

### Objectives

Create the configurable assessment foundation.

### Tasks

- Implement assessment batteries.
- Implement tests within batteries.
- Implement eligibility rules.
- Implement age/sex or other explicitly supported eligibility dimensions.
- Implement normative-dataset references.
- Implement assessment-versioning where required.
- Ensure unsupported combinations cannot be silently scored.
- Add validation for required fields and units.

### Design Rule

Eligibility should be deterministic and explainable.

The system should be able to answer:

> Why was this assessment/test available or unavailable for this participant?

### Exit Criteria

- Valid assessment batteries can be configured.
- Eligibility rules are enforced.
- Invalid tests cannot be submitted as valid scores.
- Version and normative references are retained.

---

## 7. Phase 4 — Assessment Capture Workflow

### Objectives

Build the first complete coach workflow.

### Core Flow

```text
Select participant
    ↓
Check consent/authorization
    ↓
Select eligible battery
    ↓
Start assessment session
    ↓
Enter test observations/scores
    ↓
Validate values
    ↓
Save locally
    ↓
Submit
    ↓
Server validation
    ↓
Review
    ↓
Finalize
```

### Tasks

- Participant selection.
- Assessment-session creation.
- Assessment-instance creation.
- Score entry.
- Unit/value validation.
- Required-field validation.
- Draft state.
- Submission state.
- Review state.
- Finalization state.
- Error handling.
- Audit events.
- Score revision mechanism.

### Exit Criteria

A coach can complete one valid assessment end-to-end without manual database intervention.

---

## 8. Phase 5 — Offline Assessment Capture and Sync

### Objectives

Allow assessment capture when connectivity is unreliable.

### Tasks

- Define IndexedDB stores.
- Cache required reference data.
- Store assessment drafts locally.
- Assign client-generated UUIDs.
- Add idempotency/revision identifiers.
- Queue unsynchronized changes.
- Implement synchronization.
- Detect conflicting edits.
- Prevent silent overwrites.
- Surface unresolved conflicts to an authorized user.
- Mark synchronization status clearly.

### Conflict Rule

Do not implement:

```text
last write wins
```

Instead:

```text
local change
     +
server state
     ↓
conflict detection
     ↓
explicit resolution
```

### Exit Criteria

- A coach can capture an assessment while offline.
- Refresh/reopen does not lose saved local work.
- Reconnection synchronizes valid changes.
- Duplicate submissions do not create duplicate records.
- Conflicting changes are detected rather than silently overwritten.

---

## 9. Phase 6 — Development Profile and Longitudinal History

### Objectives

Turn individual assessments into a longitudinal development record.

### Tasks

- Display assessment history.
- Display score revisions appropriately.
- Calculate supported derived metrics.
- Display normative position only where an appropriate normative dataset exists.
- Show trajectory/change over time.
- Preserve assessment context.
- Distinguish measured values from derived interpretations.
- Avoid presenting a single score as definitive talent selection.

### Exit Criteria

A participant profile can show:

- what was measured,
- when it was measured,
- under which battery/test/version,
- the recorded result,
- relevant normative context,
- change over time.

---

## 10. Phase 7 — Activity Library

### Objectives

Provide coaches with structured development activities rather than only assessment results.

### Activity Metadata

Each activity should support, where applicable:

- activity ID
- name
- domain
- age range
- objective
- difficulty
- equipment
- safety considerations
- instructions
- progression/regression
- media/video reference
- license/attribution
- evidence tags
- commercial-use status

### Tasks

- Activity data model.
- Activity administration.
- Search/filtering.
- Age/domain filtering.
- Activity detail view.
- Safety information.
- Progression information.
- Source/attribution handling.

### Exit Criteria

A coach can find an appropriate development activity and understand its purpose, requirements, safety considerations, and progression.

---

## 11. Phase 8 — Reporting

### Objectives

Produce useful outputs without turning the system into a ranking platform.

### Reports

Phase 1 reporting should prioritize:

- assessment summary
- development profile
- longitudinal change
- coach-facing observations
- participant/guardian-appropriate summary where supported
- data completeness
- assessment context

### Guardrails

- No public child leaderboard.
- No autonomous talent-selection decision.
- No medical diagnosis.
- No unsupported elite-potential claim.

### Exit Criteria

Reports are understandable, traceable to source data, and do not overstate what the assessments prove.

---

## 12. Phase 9 — Administration and Audit

### Tasks

- User administration.
- Institution administration.
- Coach/assessor verification status.
- Assessment configuration administration.
- Activity-library administration.
- Consent/audit review.
- Incident-management workflow.
- Data export where authorized.
- Data erasure workflow where applicable.
- Operational monitoring.

### Exit Criteria

An authorized administrator can manage Phase 1 configuration without direct database edits.

---

## 13. Phase 10 — Quality, Security, and Pilot Readiness

### Testing Layers

### Unit Tests

- eligibility rules
- scoring calculations
- validation
- permissions
- conflict detection
- state transitions

### Integration Tests

- API + PostgreSQL
- authentication/authorization
- assessment lifecycle
- consent lifecycle
- sync lifecycle

### End-to-End Tests

- coach login → participant → assessment → submit → review → finalize
- offline capture → reconnect → sync
- conflict detection/resolution
- unauthorized access attempts
- consent revocation

### Security Checks

- authentication
- authorization
- input validation
- session security
- secrets management
- audit logging
- rate limiting where appropriate
- secure file/media handling if introduced
- backup/recovery
- breach-response readiness

### Pilot Readiness

Before pilot:

- no known critical security issue
- no known data-loss issue
- assessment lifecycle passes end-to-end
- offline sync passes defined test cases
- audit trail works
- consent controls work
- usability test completed with representative coaches
- rollback/recovery procedure documented

---

## 14. Recommended Build Order

The implementation order should be:

```text
Repository / CI
      ↓
Identity + Roles
      ↓
Institution Authorization
      ↓
Guardian + Consent
      ↓
Assessment Configuration
      ↓
Eligibility Engine
      ↓
Assessment Capture
      ↓
Assessment Lifecycle
      ↓
Offline IndexedDB
      ↓
Sync + Conflict Resolution
      ↓
Longitudinal Development Profile
      ↓
Activity Library
      ↓
Reporting
      ↓
Admin + Audit
      ↓
Pilot Hardening
```

Do not start with dashboards, AI, video analysis, recommendations, or advanced analytics before the assessment and data lifecycle is reliable.

---

## 15. Phase 1 Definition of Done

Phase 1 is implementation-complete only when a real coach can:

1. authenticate,
2. access an authorized institution,
3. access an authorized participant,
4. confirm required consent/authorization,
5. select an eligible assessment,
6. capture assessment data,
7. save work offline,
8. synchronize safely,
9. resolve conflicts when necessary,
10. submit an assessment,
11. review/finalize it,
12. see longitudinal development information,
13. access appropriate development activities,
14. generate a traceable report,

while the system maintains appropriate authorization, consent, auditability, and data-integrity controls.

---

## 16. Explicitly Deferred

The following remain outside the Phase 1 implementation unless separately approved:

- autonomous AI talent selection
- automated video talent scoring
- elite-potential prediction
- public child rankings/leaderboards
- wearables/hardware integrations
- medical diagnosis
- premature microservices
- complex event-driven infrastructure
- large-scale recommendation engine
- broad social/community features
- direct coach-child messaging
