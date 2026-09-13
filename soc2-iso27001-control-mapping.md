# SOC 2 ↔ ISO 27001 Control Mapping (مطابقة الضوابط)

Vendors and auditors rarely speak the same framework. A vendor hands over a SOC 2 Type II report; your internal program runs on ISO/IEC 27001. Someone has to translate between them, and "trust me, they're basically the same" is not a control. This document maps a representative slice of controls between the two frameworks, at the level of rigor an auditor would expect to see cross-referenced in a control matrix.

## 1. Why the Mapping Exists (لماذا هذه المطابقة)

| Framework | Arabic | What it actually certifies |
| --- | --- | --- |
| **SOC 2** (Type II) | إطار سوك 2 | That a service organization's controls, across one or more Trust Services Criteria, operated effectively over a review period (typically 6–12 months) |
| **ISO/IEC 27001** | الأيزو 27001 | That an organization operates a certified Information Security Management System (ISMS) — a management *system*, not a fixed control list |

Neither framework is "better" — they answer different questions. SOC 2 says "here is evidence these specific controls worked, for this period, for this service." ISO 27001 says "here is a certified, audited management system that governs how controls get chosen and maintained at all." Mapping them is how GACWA compares a SOC 2 report from a cloud vendor against its own ISO 27001-aligned control set without re-inventing the vendor's evidence from scratch.

## 2. Trust Services Criteria → Annex A Control Mapping

| SOC 2 Trust Services Criteria | ISO 27001:2022 Annex A Control | Mapping Notes (ملاحظات المطابقة) |
| --- | --- | --- |
| **CC6.1** — Logical access security measures restrict access to authorized users | **A.5.15** Access control / **A.8.2** Privileged access rights | SOC 2's CC6.1 is broader than a single Annex A clause; a full mapping usually cites both the policy-level control (A.5.15) and the technical enforcement control (A.8.2) |
| **CC6.6** — The entity implements logical access security measures to protect against threats from sources outside its system boundaries | **A.8.20** Networks security / **A.8.23** Web filtering | Perimeter-facing; SOC 2 frames this as an outcome ("protected against"), ISO frames it as controls to implement — the mapping direction matters for gap analysis |
| **CC7.2** — The entity monitors system components for anomalies indicative of malicious acts, natural disasters, and errors | **A.8.16** Monitoring activities | Near 1:1 — both require active, ongoing monitoring rather than periodic review |
| **CC7.3** — The entity evaluates security events to determine whether they could or have resulted in a failure to meet objectives | **A.5.24** Information security incident management planning and preparation / **A.5.25** Assessment and decision on information security events | SOC 2 collapses detection-and-triage into one criterion; ISO splits "plan for it" (A.5.24) from "decide on this specific event" (A.5.25) |
| **CC8.1** — The entity authorizes, designs, develops, configures, documents, tests, approves, and implements changes | **A.8.32** Change management | Direct match; both require a formal, auditable change process |
| **CC9.2** — The entity assesses and manages risks associated with vendors and business partners | **A.5.19** Information security in supplier relationships / **A.5.20** Addressing information security within supplier agreements | This is the pairing that matters most for [`third-party-ai-vendor-risk-assessment.md`](third-party-ai-vendor-risk-assessment.md) — a vendor's own SOC 2 report is one input into satisfying GACWA's ISO-aligned supplier controls, not a substitute for running the assessment |
| **A1.2** (Availability criterion) — The entity authorizes, designs, develops, implements, operates, approves, maintains, and monitors environmental protections, software, data backup processes, and recovery infrastructure | **A.8.13** Information backup / **A.8.14** Redundancy of information processing facilities | SOC 2's Availability category is optional (not every SOC 2 report includes it) — the first check in any mapping exercise is confirming the vendor's report actually covers this criterion before mapping it |

## 3. Reading the Mapping (كيفية قراءة هذه المطابقة)

- **A mapping is not a translation dictionary — it's an evidence bridge.** The goal is never "SOC 2 CC6.1 equals ISO A.5.15." It's "does the evidence behind CC6.1 satisfy what our ISMS requires of A.5.15, and if not, what's the gap?"
- **Cardinality is rarely 1:1.** Most SOC 2 criteria are broader than a single Annex A control and map to two or more, as with CC6.1 and CC7.3 above. Treating every mapping as a clean 1:1 is the most common mistake in a first-pass control matrix.
- **Scope and period matter as much as the control name.** A SOC 2 report only covers the systems and time period stated on its cover page. A control "mapping" that ignores this and assumes blanket coverage is the gap an auditor will find first.
- **The Availability and Confidentiality categories are optional in SOC 2** but effectively assumed in ISO 27001's Annex A. Always confirm which Trust Services Categories a given SOC 2 report actually includes before mapping against it — see Section 2's note on A1.2.

## 4. Practical Use in This Portfolio

This mapping is the tool used in [`third-party-ai-vendor-risk-assessment.md`](third-party-ai-vendor-risk-assessment.md) to translate a vendor's SOC 2 report into GACWA's own ISO-aligned risk language, so the vendor assessment doesn't have to start from zero on every engagement.
