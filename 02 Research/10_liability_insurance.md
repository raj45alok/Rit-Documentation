# 10 — Sports Coaching Liability, Safety & Insurance (India)

> **Purpose:** Legal and practical risk landscape for youth sports coaching and assessment in India — directly informs Rit's product guardrails, terms of service, and coach-requirement checklist. **Not legal advice** — general tort principles and industry practice, not a substitute for qualified legal counsel before launch.

---

## 1. Core Legal Principles (General Tort Law, Applied to Sports)

Negligence requires three elements: **duty of care → breach of that duty → resulting injury/loss.** Indian courts apply higher scrutiny to duty of care owed to minors specifically, given their vulnerability.

| Party | Liability basis |
|---|---|
| Coach | Negligent supervision, faulty instruction, breach of duty of care |
| Academy/School | Vicarious liability for employee (coach) negligence; duty to provide a safe environment |
| Platform/software provider | **Legally unclear in Indian case law** — general principle suggests liability could attach if the platform's recommendation is negligent and causes injury, but no specific precedent was found |

**No specific Indian court cases involving youth sports academy/coach negligence were identified in this research** — the legal landscape here is thin and largely inferred from general tort principles rather than sport-specific precedent.

---

## 2. What Waivers Can and Cannot Do

- **Can:** acknowledge inherent risks of the activity; release from liability for *ordinary* negligence
- **Cannot:** release from *gross* negligence, willful misconduct, or statutory duties
- Parental consent is required for minors and should be verifiable under the DPDP Act (see `research on Child Data Privacy` — pending)

---

## 3. Insurance Landscape — Genuinely Actionable, Low-Cost

| Insurance type | Coverage | Approximate cost |
|---|---|---|
| Public liability (CGL) | Third-party injury/property damage | ₹5,000–10,000/year for ₹1 crore cover |
| Personal accident | Injury benefit regardless of fault | Under ₹2,000/year for ₹10 lakh cover |
| Professional indemnity | Poor advice/negligence claims | Varies; recommended once coaches are actively hired/engaged |
| Cyber insurance | Data breaches | Not well-documented for this sector; worth exploring given child data involved |

**Key finding:** this coverage is genuinely inexpensive relative to the risk it mitigates. Public liability cover in particular (~₹5-10k/year for ₹1 crore) is a low-cost, high-value recommendation for both Rit as a platform and any academy/coach Rit works with.

**Coaches commonly carrying insurance today:** likely uncommon at the grassroots level (not explicitly documented, but inferred from the broader fragmentation already established in `02_coach_credentialing.md`).

---

## 4. Sport-Specific Risk Notes

- **Swimming:** drowning is a significant, high-severity risk — requires lifeguards, formal safety protocols, and a materially higher duty of care. Directly relevant to the swimming feasibility research (pending) and the open-water safety module already specified in `06_talent_id_methodology.md` and `07_coach_curriculum_international.md`.
- **Boxing:** head injuries, concussion, fracture risk — requires strict safety protocols and medical supervision, consistent with the "strictly non-contact/controlled at ages 9-12" requirement already locked into the plan.

---

## 5. Child Safeguarding Legal Context

- **NCPCR guidelines** recommend police verification of sports staff, qualified coaches, and adherence to safety norms
- **POCSO Act** mandates reporting of sexual offences against children — this is a binding legal reporting obligation, not optional best practice

---

## 6. Direct Recommendations for Rit

### Terms/waivers
- Clear terms defining Rit's role as a **facilitator/infrastructure provider, not the coaching entity itself**
- Waivers acknowledging inherent activity risk, explicitly not covering gross negligence
- Verifiable parental consent (already specified as a first-class domain object in the Product Specification, Section 2.5)

### Coach requirements
- Verified credentials (already core to the Coach Credentialing module)
- **Recommend** (not necessarily mandate at MVP stage) public liability + professional indemnity insurance
- Background/police verification per NCPCR guidance
- Basic first-aid/CPR certification requirement

### Assessment safety rules
- Pre-assessment risk check (environment, equipment, child readiness)
- Defined coach-to-child supervision ratios
- Explicit "stop rules" — coach must halt if a child shows distress or unsafe movement

### Product features that REDUCE liability
Human-in-the-loop review of any AI output; clear, prominent safety warnings; progression locks (advanced activities gated until basics are mastered); easy incident logging; verifiable consent management.

### Product features that INCREASE liability — avoid or tightly constrain
Autonomous AI recommendations without human review; prescriptive training that ignores individual context; public child leaderboards (already excluded in the Product Specification, Section 2.18); inadequate/missing risk warnings.

### Incident logging (already specified in Product Specification 2.14)
This research confirms the specified incident-record structure (athlete, session, category, severity, description, immediate action, parent notification, referral, review status) matches actual risk-management practice — no changes recommended, this was built correctly the first time.

---

## Sources
- General Indian tort law principles applicable to negligence claims
- NCPCR child safeguarding guidelines for sports settings
- POCSO Act reporting obligations
- Insurance product research (public liability, personal accident, professional indemnity — Indian market)
- Khelo India Scheme Operational Guidelines (MoU/grantee framework, referenced for institutional liability context)

**Caveat:** this research found limited India-specific case law directly on point for youth sports/coaching negligence. Legal counsel should review Rit's actual terms of service and waiver language before any public launch — this document is risk-awareness research, not a legal opinion.

---

*Previous: [`09_coach_adoption_incentives.md`](./09_coach_adoption_incentives.md) · Next: [`11_government_partnerships.md`](./11_government_partnerships.md)*
