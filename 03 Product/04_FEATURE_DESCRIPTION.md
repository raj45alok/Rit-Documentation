# Rit --- Feature Description

## 1. Authentication

Phone/OTP authentication with rate limits, short-lived access tokens,
refresh sessions and revocation. Implementation is provider-independent.

## 2. Coach verification

Identity gateway → credentials → safeguarding → institution association
→ verification status.

Rit verification must not imply government/federation accreditation.

## 3. Institution management

Institution profile, memberships, roles, batches/rosters, lead assessor
and operational reporting.

## 4. Guardian/DataSubject

Guardian verification, child relationship, institution authorization,
immutable consent events and withdrawal.

## 5. Eligibility Engine

Determines battery eligibility from DOB, assessment date,
methodology/version, authorization and explicit rules. Returns reason
and rule version.

## 6. Assessment session

Separates assessment logistics from an individual child's assessment.

## 7. Assessment capture

Guided tests, safety checks, attempts, measurements,
observations/context, autosave and lifecycle controls.

## 8. Offline sync

IndexedDB → local mutation queue → immutable revisions → server
validation → acceptance/rejection/conflict → explicit resolution.

LWW is forbidden.

## 9. Review/finalization

DRAFT → SUBMITTED → REVIEWED → FINALIZED with optimistic concurrency and
audit history.

## 10. Development profile

Measurements + defensible reference context + trajectory + strengths +
development areas + coach observations + goals.

No Phase 1 talent score.

## 11. Coach feedback

Structured observation, strength, development area, goal, practice
suggestion and review date.

## 12. Activity library

Search/filter by age stage, objective, domain, equipment and difficulty.
Activities include safety/evidence/licensing metadata.

## 13. Reports

Guardian-facing report contains measurements, reference context,
longitudinal comparison, coach feedback and goals. Avoid harmful ranking
language.

## 14. Incident management

Create, classify, assign, investigate, escalate, resolve and audit.

## 15. Audit

Audit authentication/security, consent, sensitive access, assessment
lifecycle, deletion, administration and conflict resolution. No child
PII in metadata.

## 16. Erasure

Authenticated request → authorization → deletion workflow → associated
record/storage cleanup → verification → minimal audit.

## 17. Authorization

Role check plus relationship/institution authorization. Frontend
visibility is not a security boundary.

## 18. Notifications

Minimal Phase 1 notifications. Avoid unnecessary child details.

## 19. Observability

Measure API failures, authentication abuse, sync reliability/conflicts,
assessment lifecycle, report failures and deletion-job failures.

## 20. Phase 2

Development plans, recommendations, coach learning, session planning,
expanded library, reassessment analytics and phone-video R&D.

## 21. Phase 3

Sport orientation, sport-specific assessment, competitions,
opportunities, progression/pathways and mature analytics.

## 22. Feature guardrails

No public rankings, autonomous talent decisions, medical diagnosis,
AI-only coaching, marketplace/payment infrastructure, social feed or
unapproved government dependency.
