# Rit --- Consolidated Product Specification

This is the consistency baseline for the five engineering/product
documents.

## 1. Product

A secure, web-only, coach-mediated longitudinal youth sports assessment
and development platform for India.

## 2. Core loop

``` text
Guardian authorization
 ↓
Assessment
 ↓
Measurement
 ↓
Development profile
 ↓
Coach feedback
 ↓
Goal
 ↓
Practice/activity
 ↓
Reassessment
 ↓
Trajectory
```

Phase 1 implements the assessment, profile, feedback and reporting
foundation. Training-loop depth grows later.

## 3. Phase boundaries

### Phase 1 --- Foundation

Authentication, identity/coach verification, institution,
guardian/DataSubject, authorization/consent, standardized assessments,
offline capture, sync/conflict resolution, review/finalization,
longitudinal history, feedback, activity library, reports, incidents,
audit/privacy.

### Phase 2 --- Development

Development plans, recommendations, coach learning, expanded activity
library, session planning, reassessment analytics and phone-video
research.

### Phase 3 --- Ecosystem

Sport orientation, sport-specific assessment, competition records,
opportunities, progression/pathways, institutional ecosystem and mature
analytics.

## 4. Role model

Guardian controls child relationship/consent and reports.

Assessor performs authorized assessments and provides feedback.

Institution admin manages institutional operations and access.

Platform admin manages verification, safeguarding, support and audit.

Child is a DataSubject and has no Phase 1 login.

## 5. UX principles

-   Minimize typing.
-   One primary action per screen where practical.
-   Make offline state visible.
-   Never hide conflicts.
-   Explain what is measured.
-   Avoid harmful labels.
-   Keep guardian reports understandable.
-   Keep assessment workflows fast.
-   Responsive and accessible web design.

## 6. Report model

Separate: 1. Measurement. 2. Reference context. 3. Developmental
interpretation. 4. Suggested action.

Automated text cannot imply diagnosis or guaranteed athletic potential.

## 7. Data lifecycle

``` text
Collected
 ↓
Validated
 ↓
Revised when necessary
 ↓
Reviewed
 ↓
Finalized
 ↓
Longitudinal use
 ↓
Retention/erasure policy
```

## 8. Quality gates

Before implementation: - every entity maps to a feature; - every feature
maps to a flow; - every flow maps to API/use cases; - sensitive
operations map to authorization; - offline mutations map to sync
rules; - deletion maps to cleanup; - historical records map to
versioning; - Phase 2/3 features remain separated.

## 9. Product guardrails

Rit must not claim that: - one test predicts elite success; - Rit
replaces a qualified coach; - scores diagnose medical conditions; - Rit
verification equals government accreditation; - k=5 is automatically
legally sufficient anonymization; - recommendations are official
selection decisions.

## 10. Open decisions before pilot

-   exact identity providers;
-   final assessment batteries/tests and licensing;
-   final privacy/legal review;
-   retention schedule;
-   guardian verification procedure;
-   credential-document retention;
-   notification provider;
-   hosting provider;
-   pilot institutions/geography;
-   primary user validation.

## 11. Definition of Phase 1 done

A verified assessor can conduct a complete assessment; a guardian can
authorize/revoke access; assessment survives connectivity loss; sync is
idempotent; conflicts are explicitly resolved; authorization is enforced
server-side; finalized data is reproducible; reports use finalized data;
deletion is tested; audit logs contain no child PII; backups/restoration
are tested; critical domain rules have automated tests; production
monitoring exists.

## 12. Final baseline

> Rit Phase 1 is a secure web-only modular monolith using
> Next.js/TypeScript, FastAPI/Python, PostgreSQL and IndexedDB-based
> offline assessment capture.

The product remains deliberately narrow so that real-world validation
can determine later expansion.
