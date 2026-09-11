# 09 — Implementation Checklist

## 1. How to Use This Checklist

This is the execution and verification checklist for Rit.

Use:

- `[ ]` not started
- `[x]` completed
- `[~]` in progress
- `[!]` blocked or requires decision

A feature should not be considered complete merely because the UI works. It must satisfy the relevant data, authorization, validation, offline, audit, testing, and product guardrails.

---

# 2. Repository and Engineering Foundation

- [ ] Separate Rit application repository created
- [ ] Documentation repository remains separate
- [ ] Frontend project initialized
- [ ] Backend project initialized
- [ ] PostgreSQL development database configured
- [ ] SQLAlchemy configured
- [ ] Alembic configured
- [ ] Environment-variable strategy documented
- [ ] Secrets excluded from Git
- [ ] Linting configured
- [ ] Formatting configured
- [ ] Type checking configured
- [ ] Unit-test framework configured
- [ ] Integration-test framework configured
- [ ] End-to-end test framework configured
- [ ] CI pipeline created
- [ ] Local development setup documented

---

# 3. Architecture

- [ ] Next.js + TypeScript confirmed
- [ ] FastAPI + Python confirmed
- [ ] PostgreSQL confirmed
- [ ] IndexedDB selected for browser offline storage
- [ ] Modular monolith structure established
- [ ] REST/JSON API conventions documented
- [ ] Provider abstractions established where required
- [ ] No unnecessary microservices introduced
- [ ] No unnecessary Redis/queue dependency introduced
- [ ] Object storage introduced only when required

---

# 4. Identity and Access

- [ ] User model implemented
- [ ] Authentication implemented
- [ ] Role model implemented
- [ ] Coach/assessor profile implemented
- [ ] Institution model implemented
- [ ] Institution membership implemented
- [ ] Server-side authorization implemented
- [ ] Cross-institution access blocked
- [ ] Unauthorized participant access blocked
- [ ] Security-sensitive actions audited
- [ ] Authorization tests written

---

# 5. Guardian and Participant Data

- [ ] Data-subject model implemented
- [ ] Guardian profile implemented
- [ ] Guardian ↔ participant relationship implemented
- [ ] Institution authorization represented
- [ ] Participant identifiers use non-guessable IDs
- [ ] Sensitive participant data is not unnecessarily exposed
- [ ] Access rules tested
- [ ] Data lifecycle documented

---

# 6. Consent and Safeguarding

- [ ] Consent-event model implemented
- [ ] Required guardian consent workflow implemented
- [ ] Consent status visible to authorized users
- [ ] Consent timestamps recorded
- [ ] Consent revocation workflow implemented
- [ ] Restricted actions after revocation implemented
- [ ] Incident-report model implemented
- [ ] Incident lifecycle implemented
- [ ] Safeguarding-sensitive actions audited
- [ ] Direct uncontrolled coach-child messaging excluded
- [ ] Child media access controlled
- [ ] Safeguarding test cases completed

---

# 7. Assessment Configuration

- [ ] Assessment battery model implemented
- [ ] Assessment test model implemented
- [ ] Battery eligibility rule model implemented
- [ ] Normative dataset model implemented
- [ ] Assessment versions represented
- [ ] Test units represented
- [ ] Required fields validated
- [ ] Invalid values rejected
- [ ] Unsupported participant/test combinations rejected
- [ ] Eligibility decisions are explainable
- [ ] Eligibility tests completed

---

# 8. Assessment Lifecycle

## State Model

```text
DRAFT
  ↓
SUBMITTED
  ↓
REVIEWED
  ↓
FINALIZED
```

- [ ] Draft state implemented
- [ ] Submit transition implemented
- [ ] Review transition implemented
- [ ] Finalize transition implemented
- [ ] Invalid state transitions rejected
- [ ] Finalized records protected from silent modification
- [ ] Corrections use revision mechanism
- [ ] Revision history retained
- [ ] Audit events recorded
- [ ] Lifecycle tests completed

---

# 9. Assessment Capture

- [ ] Participant selection implemented
- [ ] Consent/authorization check before assessment
- [ ] Eligible battery selection implemented
- [ ] Assessment session creation implemented
- [ ] Test-score entry implemented
- [ ] Unit validation implemented
- [ ] Range validation implemented
- [ ] Required-field validation implemented
- [ ] Draft save implemented
- [ ] Submission validation implemented
- [ ] Error messages are understandable
- [ ] Assessment can be completed without database intervention

---

# 10. Offline Capability

- [ ] IndexedDB schema defined
- [ ] Required reference data cache defined
- [ ] Assessment drafts stored locally
- [ ] Local records have stable IDs
- [ ] Sync queue implemented
- [ ] Sync status visible to user
- [ ] Offline changes survive refresh
- [ ] Offline changes survive browser restart where supported
- [ ] Reconnection triggers safe synchronization
- [ ] Duplicate submissions prevented
- [ ] Failed synchronization is retryable
- [ ] Unsynchronized work is clearly indicated

---

# 11. Conflict Resolution

- [ ] Server revision/version represented
- [ ] Client revision/idempotency identifier represented
- [ ] Conflicting updates detected
- [ ] Last-write-wins NOT used for assessment records
- [ ] Conflict state represented
- [ ] Authorized resolution workflow implemented
- [ ] Resolution is auditable
- [ ] User is informed when manual resolution is required
- [ ] Conflict tests completed

---

# 12. Longitudinal Development Profile

- [ ] Assessment history displayed
- [ ] Assessment dates displayed
- [ ] Test/battery context displayed
- [ ] Score revisions represented correctly
- [ ] Supported derived metrics calculated
- [ ] Normative position shown only where supported
- [ ] Trajectory/change shown over time
- [ ] Context/observations retained
- [ ] Measured values distinguished from interpretations
- [ ] No single-score talent claim presented
- [ ] No unsupported elite-potential prediction presented

---

# 13. Activity Library

- [ ] Activity model implemented
- [ ] Activity ID
- [ ] Activity name
- [ ] Domain
- [ ] Age range
- [ ] Objective
- [ ] Difficulty
- [ ] Equipment
- [ ] Safety considerations
- [ ] Instructions
- [ ] Progression/regression
- [ ] Media/video reference where applicable
- [ ] License/attribution
- [ ] Evidence tags
- [ ] Commercial-use status
- [ ] Search implemented
- [ ] Filtering implemented
- [ ] Activity detail page implemented
- [ ] Safety information clearly visible

---

# 14. Reporting

- [ ] Assessment summary implemented
- [ ] Development profile implemented
- [ ] Longitudinal change included
- [ ] Coach observations included where appropriate
- [ ] Participant/guardian summary designed appropriately
- [ ] Data completeness surfaced
- [ ] Report values trace back to source records
- [ ] No public child leaderboard
- [ ] No autonomous talent-selection decision
- [ ] No medical diagnosis
- [ ] No unsupported claims

---

# 15. Administration

- [ ] User administration
- [ ] Institution administration
- [ ] Coach/assessor verification status
- [ ] Assessment configuration administration
- [ ] Activity-library administration
- [ ] Consent/audit review
- [ ] Incident-management workflow
- [ ] Authorized data export
- [ ] Authorized data-erasure workflow
- [ ] Operational monitoring

---

# 16. Auditability

- [ ] Authentication/security events audited where required
- [ ] Consent events audited
- [ ] Assessment lifecycle events audited
- [ ] Score revisions audited
- [ ] Conflict resolutions audited
- [ ] Administrative changes audited
- [ ] Incident actions audited
- [ ] Audit records cannot be silently overwritten
- [ ] Audit access is restricted

---

# 17. Testing

## Unit

- [ ] Eligibility rules
- [ ] Validation rules
- [ ] Scoring calculations
- [ ] Permission checks
- [ ] State transitions
- [ ] Revision handling
- [ ] Conflict detection

## Integration

- [ ] Authentication + database
- [ ] Authorization + institution boundary
- [ ] Assessment lifecycle
- [ ] Consent lifecycle
- [ ] Offline sync
- [ ] Conflict handling
- [ ] Reporting

## End-to-End

- [ ] Coach login → participant → assessment → submit
- [ ] Assessment → review → finalize
- [ ] Offline capture → reconnect → sync
- [ ] Duplicate sync attempt
- [ ] Conflict detection → resolution
- [ ] Consent revocation → restricted action
- [ ] Unauthorized cross-institution access
- [ ] Admin configuration flow

---

# 18. Security

- [ ] Authentication secured
- [ ] Authorization server-side
- [ ] Input validation
- [ ] Secure session handling
- [ ] Secrets management
- [ ] Database credentials protected
- [ ] Sensitive logs reviewed
- [ ] Rate limiting considered/implemented where appropriate
- [ ] File/media handling secured if introduced
- [ ] Backup strategy documented
- [ ] Restore procedure tested
- [ ] Incident-response procedure documented
- [ ] No child data exposed in public URLs
- [ ] No sensitive data unnecessarily stored client-side

---

# 19. Performance and Reliability

- [ ] Assessment form remains usable on lower-end devices
- [ ] Large assessment history does not freeze the UI
- [ ] Offline capture remains responsive
- [ ] Sync retries safely
- [ ] API errors handled gracefully
- [ ] Database indexes reviewed
- [ ] Backup monitoring implemented
- [ ] Error monitoring implemented
- [ ] Critical failures are observable

---

# 20. UX / Coach Adoption

- [ ] Coach can understand what to do without technical training
- [ ] Assessment workflow minimizes unnecessary steps
- [ ] Important validation errors are actionable
- [ ] Offline status is visible
- [ ] Sync status is visible
- [ ] Conflict messages are understandable
- [ ] Assessment instructions are clear
- [ ] Safety information is easy to find
- [ ] Reports are understandable
- [ ] Pilot usability test completed
- [ ] Pilot feedback recorded
- [ ] High-friction workflow issues addressed

---

# 21. Pilot Readiness Gate

All of the following must be true:

- [ ] No known critical security issue
- [ ] No known critical data-loss issue
- [ ] End-to-end assessment workflow passes
- [ ] Offline assessment workflow passes
- [ ] Sync workflow passes
- [ ] Conflict handling passes
- [ ] Consent workflow passes
- [ ] Authorization tests pass
- [ ] Audit trail works
- [ ] Backup/recovery tested
- [ ] Representative coach usability test completed
- [ ] Pilot support process documented
- [ ] Rollback/recovery procedure documented
- [ ] Product guardrails reviewed
- [ ] Phase 1 scope confirmed

---

# 22. Explicit Scope Guardrails

Do not mark Phase 1 complete by adding these prematurely:

- [ ] No autonomous AI talent selection
- [ ] No automated video talent scoring
- [ ] No elite-potential prediction
- [ ] No public child ranking
- [ ] No wearables/hardware requirement
- [ ] No medical diagnosis
- [ ] No premature microservices
- [ ] No unnecessary event-driven infrastructure
- [ ] No complex recommendation engine
- [ ] No uncontrolled direct coach-child messaging

---

# 23. Final Phase 1 Sign-Off

A Phase 1 release should not be signed off until the team can demonstrate:

- [ ] Authorized coach can access an authorized participant
- [ ] Required consent/authorization is respected
- [ ] Eligible assessment can be selected
- [ ] Assessment can be captured
- [ ] Assessment can be captured offline
- [ ] Offline data can synchronize safely
- [ ] Conflicts are not silently overwritten
- [ ] Assessment can move through its lifecycle
- [ ] Revisions remain traceable
- [ ] Longitudinal profile is available
- [ ] Development activities are available
- [ ] Report is traceable and appropriately bounded
- [ ] Safeguarding and audit controls operate
- [ ] Security tests pass
- [ ] Pilot usability criteria pass

**Phase 1 status:** `[ ] READY FOR PILOT`
