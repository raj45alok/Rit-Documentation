# 14 — Child Data Privacy & Safeguarding: DPDP Act 2023 and Architecture Requirements

> **Purpose:** Legal and regulatory foundation directly determining Rit's data model, consent flows, and access-control architecture. **This document does not constitute legal advice** — clearly distinguish statutory requirement from recommended practice; have qualified counsel review actual implementation before launch.

---

## 1. Digital Personal Data Protection Act, 2023 (DPDP Act) — Core Requirements

| Element | Requirement |
|---|---|
| Child definition | Under 18 years of age |
| Consent | **Verifiable parental/guardian consent mandatory** before processing any child's personal data |
| Prohibited processing | Tracking or behavioural monitoring of children; targeted advertising to children |
| Retention | Data retained only as long as necessary for the stated purpose |
| Breach obligations | Must notify the Data Protection Board and affected users per prescribed rules |
| Penalties | Significant, including specifically for failure to obtain verifiable parental consent |

**Status: this Act is enacted and in force.** The **DPDP Rules, 2025 were notified in November 2025** — these prescribe the actual mechanics of "verifiable parental consent," including due diligence to verify the identity and age of the parent. This is current, binding, operational law, not a future/pending requirement.

---

## 2. Important Nuance Requiring Legal Review

The Act prohibits **"tracking or behavioural monitoring of children."** This term is most directly aimed at online/ad-tech-style behavioral tracking. **Whether Rit's longitudinal athletic-development tracking (repeated physical assessments over months/years) falls under this prohibition is not clearly resolved by available research** and should be specifically reviewed with counsel before finalizing the data model. This is flagged as an open legal question, not a resolved one — treat with genuine caution rather than assuming it doesn't apply.

---

## 3. Related Legal Framework

- **POCSO Act, 2012** — mandates reporting of sexual offences against children; NCPCR provides a POCSO e-box reporting mechanism
- **IT Rules, 2021 (Intermediary Guidelines)** — requires removal of unlawful content, including content violating child-protection law
- **NCPCR guidance** — recommends police verification of sports staff, qualified/trained coaches, adherence to safety norms in school/SAI training-centre contexts

---

## 4. Direct Answers to Key Architecture Questions

| Question | Answer |
|---|---|
| Is there a separate "sensitive data" category for fitness/health data? | **No** — DPDP does not create a distinct sensitive-data category, but *all* children's data carries heightened obligations regardless of type |
| What about video/photos of children? | Requires the same verifiable parental consent; must avoid tracking/behavioural monitoring; must not be used for targeted advertising |
| Should coach-child direct messaging be permitted? | **No** — should be avoided or strictly controlled, with parent/guardian involvement and audit logs |
| What happens at age 18? | The individual becomes an adult Data Principal; consent/processing basis must be reviewed and updated |
| Cross-border/cloud storage? | Permitted except to government-restricted countries; must have appropriate safeguards |
| Third-party AI API vendors? | Data Fiduciary (Rit) remains responsible for compliance even when using third-party processors |

---

## 5. Access Control Model (Confirmed by This Research)

- **Parents/guardians:** full access to their child's data (as Data Principals)
- **Coaches:** access limited to athletes they actually coach, with appropriate safeguards
- **Institutions:** administrative/safety-purpose access, with audit logs

This directly validates the role-based access model already specified in the Product Specification (Coach / Parent-Guardian / Athlete / Institution Administrator / Rit Administrator) — no architectural change needed, just confirmation that it's legally required, not just good design.

---

## 6. Product & Architecture Requirements (Translated from Legal Findings)

### A. Legal requirements (non-negotiable)
- Verifiable parental consent before any child data processing — including photos/video
- No behavioural tracking/monitoring in the ad-tech sense (see open question above)
- No targeted advertising involving children's data
- Data retained only as long as necessary; deletion mechanism required
- Consent withdrawal mechanism required
- Breach notification process to the Data Protection Board

### B. Recommended best practice beyond minimum legal requirement
- Treat consent as a first-class versioned domain object (already specified in Product Spec 2.5) — not just a checkbox
- Separate consent specifically for photo/video from general data-processing consent
- Maintain audit logs on all sensitive-data access, not just breaches

### C. High-risk features to avoid or tightly constrain
- Unrestricted direct coach-child messaging (avoid entirely, or heavily gate with parent visibility)
- Public leaderboards/profiles involving identifiable child data (already excluded in Product Spec)
- Any behavioral-tracking-style feature (recommendation engines, engagement-optimization patterns) applied to children — flagged as the open legal question above

### D. Data minimization
Collect only what the athlete profile actually needs (name, DOB, sex, guardian relationship, institution, sport participation) — already the stated principle in Product Spec Section 2.4; this research confirms it as legally load-bearing, not just good hygiene.

### E. Retention/deletion model
Retention period tied explicitly to purpose; deletion workflow must exist and be triggered by consent withdrawal or purpose completion, "unless required by law" (e.g., safeguarding-incident records may need longer retention — reconcile these two obligations carefully in the actual data-retention policy).

### F. Practical privacy-by-design checklist for MVP
- [ ] Verifiable parental consent flow (per DPDP Rules 2025 mechanics) built before any child profile can be created
- [ ] Separate, explicit consent toggle for photo/video (if used at all in Phase 1 — note Phase 1 per Product Spec already excludes phone-video assessment)
- [ ] Role-based access strictly enforced (coach sees only their own athletes)
- [ ] Audit log on all child-data access
- [ ] Deletion/withdrawal workflow functional before launch, not added later
- [ ] Legal review specifically on whether longitudinal assessment tracking constitutes "behavioural monitoring" under DPDP

---

## Sources
- Digital Personal Data Protection Act, 2023
- Digital Personal Data Protection Rules, 2025 (notified November 2025)
- POCSO Act, 2012
- IT (Intermediary Guidelines and Digital Media Ethics Code) Rules, 2021
- NCPCR guidelines for protection of children in SAI training centres and schools

**This document is risk-awareness and architecture-planning research, not legal advice.** Engage qualified counsel to review actual consent flows, retention policy, and the behavioural-monitoring question before public launch.

---

*Previous: [`13_swimming_feasibility_haryana.md`](./13_swimming_feasibility_haryana.md) · Next: [`15_coach_credentialing_gap_india.md`](./15_coach_credentialing_gap_india.md)*
