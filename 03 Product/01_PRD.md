# Rit --- Product Requirements Document

**Status:** Phase 1 baseline\
**Platform:** Web-only\
**Target:** Indian youth sports development, ages 6--16

## 1. Product definition

Rit is a coach-mediated youth sports development platform that creates a
trustworthy longitudinal record of assessment, development, feedback and
progression.

Phase 1 is intentionally narrow: **standardized assessment, longitudinal
tracking, structured coach feedback, safe guardian visibility and
reliable offline-capable assessment capture.**

Rit is not a talent-selection authority, medical system, social network,
marketplace, government replacement or autonomous AI coach.

## 2. Product principles

-   Evidence before assumptions.
-   Development before selection.
-   Trajectory before one-day ranking.
-   Human coaching remains responsible for interpretation.
-   Privacy and safeguarding are first-class requirements.
-   Offline assessment is required even though the product is web-only.
-   No silent overwrites.
-   No public child leaderboards.
-   No autonomous AI decisions.
-   Technical complexity must be justified by product requirements.

## 3. Users

### Guardian

Manages the child relationship and consent and views authorized reports.

### Coach / Assessor

Verified professional who conducts assessments, records observations and
provides structured feedback.

### Institution Administrator

Manages institution membership, rosters, authorization and
operational/safeguarding workflows.

### Child / Data Subject

The child whose data is processed. No direct account in Phase 1.

### Platform Administrator

Handles verification, safeguarding, support and platform operations.

## 4. Core Phase 1 workflow

Coach verification → institution → batch/roster → guardian invitation →
guardian verification/authorization → assessment → offline capture →
sync → review → finalization → report → feedback/goals → longitudinal
history.

## 5. Assessment requirements

Assessment batteries and tests are versioned and immutable.

Each assessment stores: - battery/test version; - assessment date; - raw
measurements; - attempts where applicable; - observations/context; -
assessor; - normative dataset version where used; - lifecycle state; -
revision history.

Eligibility is evaluated by an Eligibility Engine, not by hard-coded
frontend age branches.

Phase 1 does not produce a single talent score.

## 6. Development profile

The profile contains: - measured results; - reference context where
defensible; - individual trajectory; - strengths; - development areas; -
coach observations; - goals; - suggested practice.

Avoid harmful labels such as failure, poor, elite or guaranteed talent.

## 7. Activity library

Activities contain age/development stage, objective, difficulty,
equipment, instructions, progression/regression, safety, evidence
status, attribution/licensing and media references.

## 8. Safeguarding

Required: - coach safeguarding status; - controlled child-record
access; - incident reporting and triage; - parent visibility where
appropriate; - no unrestricted coach-child direct messaging; -
assessment safety/abort controls.

Rit does not diagnose or treat medical conditions.

## 9. Privacy

Design requirements: - verifiable guardian consent; - data
minimization; - purpose limitation; - server-side authorization; -
auditability; - controlled retention and erasure; - secure storage; - no
targeted advertising to children; - no public child profiles or
leaderboards.

Legal claims must be separately verified.

## 10. Offline requirements

The browser must support: - cached authorized roster; - assessment
definitions; - local assessment capture; - durable pending mutations; -
retry; - conflict detection; - explicit conflict resolution.

Use IndexedDB or an equivalent durable browser store.

## 11. Phase 1 non-goals

-   AI talent prediction
-   autonomous AI coaching
-   phone-video assessment
-   wearables
-   payments
-   marketplace
-   public leaderboards
-   social network
-   nutrition diagnosis
-   medical records
-   competition management
-   national coach licensing
-   government API dependency
-   advanced sport-specific talent selection

## 12. Success measures

Track assessment completion, sync reliability, conflict rate,
finalization rate, report generation, data-integrity defects,
safeguarding resolution, second-cycle completion and guardian/coach
usefulness.

Pilot targets should be established from baseline rather than invented.

## 13. Locked Phase 1 technology direction

-   Next.js + TypeScript
-   Python + FastAPI
-   PostgreSQL
-   IndexedDB for web offline capture
-   Modular monolith
-   REST API
-   identity-provider abstraction
-   append-only revisions
-   explicit conflict resolution
-   no LWW
