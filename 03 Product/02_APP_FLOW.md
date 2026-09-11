# Rit --- Application Flow

## 1. Primary flows

``` text
Coach
 → Authentication
 → Verification
 → Institution
 → Batch/Roster
 → Guardian invitation
 → Assessment
 → Offline capture
 → Sync
 → Review
 → Finalize
 → Report/Feedback

Guardian
 → Authentication
 → Invitation
 → Verification
 → Child relationship
 → Consent
 → Report
 → Consent management / erasure

Admin
 → Authentication
 → Coach verification
 → Institution administration
 → Incidents
 → Audit/support
```

## 2. Coach onboarding

OTP → profile → identity-verification gateway → credentials →
safeguarding → institution association → admin review where required →
authorized/pending/rejected.

A provider such as DigiLocker remains an implementation option behind an
identity gateway, not a hard-coded product dependency.

## 3. Institution and guardian flow

Coach selects institution → creates batch/roster → sends guardian
invitation → guardian authenticates/verifies → confirms child
relationship → authorization/consent event recorded.

`AssessmentSession` represents logistics. `AssessmentInstance`
represents one child's assessment.

## 4. Eligibility flow

The client requests eligibility from the server using DOB, assessment
date, battery/version and authorization context. The Eligibility Engine
returns eligible/ineligible plus the rule version/reason.

## 5. Assessment flow

Session → child → safety check → eligibility → battery instructions →
test execution → save locally after meaningful mutations → review →
submit.

The workflow must survive refresh and temporary connectivity loss.

## 6. Offline flow

``` text
Online
 ↓
Cache minimum authorized roster + definitions
 ↓
Connectivity lost
 ↓
Capture locally in IndexedDB
 ↓
Queue immutable revisions
 ↓
Connectivity restored
 ↓
Sync
 ↓
Server authorization/version/conflict checks
 ↓
Accepted / rejected / conflict
```

No last-write-wins.

## 7. Conflict flow

``` text
          Revision A
          /             Revision B   Revision C
          \        /
           CONFLICT
              ↓
       Lead assessor review
              ↓
        Choose reality
              ↓
      Resolved current revision
```

All branches remain auditable according to retention policy.

## 8. Assessment lifecycle

``` text
DRAFT → SUBMITTED → REVIEWED → FINALIZED
```

Invalid transitions are rejected. Finalization uses optimistic
concurrency.

## 9. Guardian report

Guardian → child → finalized assessment → measured results → reference
context → trajectory → strengths/development areas → coach feedback →
goals/practice.

No public ranking.

## 10. Consent revocation

Guardian revokes → server authorization becomes revoked → new
server-side assessment mutations rejected → next sync informs offline
client → unauthorized local child data is removed from active
roster/cache.

Exact treatment of already-captured offline data follows the finalized
privacy/legal policy.

## 11. Erasure

Authenticated request → authorization check → deletion job → delete
eligible child-associated personal data → clean storage/cache → verify →
minimal audit event.

Only genuinely anonymous independent aggregates may survive.

## 12. Incident flow

Create → classify severity → assign → investigate → action/escalation →
resolve → audit.

Use structured severity/status values.
