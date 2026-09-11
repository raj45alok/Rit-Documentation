# Rit --- Database Schema

**Database:** PostgreSQL

## 1. Core model

``` text
User
 ├─ GuardianProfile
 └─ AssessorProfile

Institution
 └─ InstitutionMembership

DataSubject
 └─ DataSubjectGuardian

InstitutionAuthorization
 └─ ConsentEvent

AssessmentBattery
 └─ AssessmentTest
      └─ BatteryEligibilityRule

AssessmentSession
 └─ AssessmentInstance
      └─ TestScoreRevision

NormativeDataset
ActivityLibrary
IncidentReport
AuditEvent
```

## 2. User

`id UUID PK`, login identifier, status, timestamps.

## 3. GuardianProfile

`user_id PK/FK`, verification status/provider/reference, timestamps.

## 4. AssessorProfile

`user_id PK/FK`, profile data, verification status, safeguarding status,
credential summary, timestamps.

Credential artifacts should be separated from profile data.

## 5. Institution

`id`, name, type, status, metadata, timestamps.

## 6. InstitutionMembership

`id`, institution_id, user_id, role, status, valid_from, valid_to,
timestamps.

## 7. DataSubject

`id`, minimal required identifying data, DOB, sex where methodology
requires it, height/weight only where justified, status, timestamps.

No login credentials.

## 8. DataSubjectGuardian

`id`, data_subject_id, guardian_user_id, relationship, primary flag,
validity/status fields.

Use a junction table even if Phase 1 normally has one primary guardian.

## 9. InstitutionAuthorization

Mutable current state: - id - institution_id - data_subject_id -
guardian_user_id - status ACTIVE/REVOKED/EXPIRED -
granted_at/revoked_at - timestamps

## 10. ConsentEvent

Immutable ledger: - id - authorization_id - actor - event_type -
policy_version - legal_text_hash - occurred_at - verification_method -
evidence reference if needed

## 11. AssessmentBattery

Immutable: - id - logical_key - version - name - status -
definition_json - timestamps

## 12. AssessmentTest

Immutable: - id - battery_id - logical_key - version - name -
measurement type - instructions/scoring/safety definitions - timestamps

## 13. BatteryEligibilityRule

-   id
-   battery_id
-   rule_version
-   age boundaries
-   rule_json
-   status

Cross-table eligibility is enforced by the domain engine; database
constraints enforce structural validity.

## 14. AssessmentSession

-   id
-   institution_id
-   lead_assessor_id
-   batch/reference
-   scheduled_at
-   status
-   timestamps

## 15. AssessmentInstance

-   id
-   assessment_session_id
-   data_subject_id
-   battery_id
-   status
-   optimistic-lock version
-   lifecycle timestamps

## 16. TestScoreRevision

Append-only: - id - assessment_instance_id - assessment_test_id -
client_revision_id UNIQUE - parent_revision_id nullable - device_id -
client revision metadata - score_json - observation_json -
context_json - created_by - created_at - sync_state -
conflict_group_id - resolution metadata

## 17. NormativeDataset

Store dataset identity, version, population, methodology,
source/reference and validity metadata.

Historical assessments reference the exact version used.

## 18. ActivityLibrary

Store title, domain, age stage, objective, difficulty, equipment,
instructions, progression, regression, safety, evidence status,
licensing/attribution, media reference and status.

## 19. IncidentReport

Store institution, subject where appropriate, reporter, severity,
status, occurrence time, structured facts, resolution and timestamps.
Minimize sensitive free text.

## 20. AuditEvent

Store id, timestamp, actor, action, entity type/id, correlation ID, IP
hash where justified, metadata JSON.

Never duplicate child PII into audit metadata.

## 21. Critical invariants

-   UUID primary keys.
-   Foreign keys.
-   Unique constraints.
-   Immutable assessment definitions.
-   Append-only score revisions.
-   Append-only consent events.
-   Append-only audit events.
-   Server-side authorization.
-   No cross-institution access without active authorization.
-   Finalized results cannot be silently changed.
-   Client revision IDs are idempotent.
-   Conflicts are preserved.
-   Deletion is explicitly tested.
-   Anonymous aggregates contain no direct identifiers.

## 22. Initial indexes

Index authentication identifier, institution membership, guardian
relationships, authorization, assessment subject/date, session, score
revision lookup and audit entity/time.

Add indexes based on measured query patterns.
