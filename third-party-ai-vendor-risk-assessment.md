# Third-Party AI Vendor Risk Assessment (تقييم مخاطر مورد الذكاء الاصطناعي)

*Hypothetical vendor engagement for the Global Air Cargo & Warehousing Authority*

Approving a vendor because "the sales deck looked thorough" is not a risk assessment. This document walks through evaluating a hypothetical AI vendor against data handling, model transparency, and SLA criteria, using the SOC 2 ↔ ISO 27001 mapping from [`soc2-iso27001-control-mapping.md`](soc2-iso27001-control-mapping.md) as the evidence bridge.

## 1. Scenario (السيناريو)

**Vendor:** "ClearFlow AI" (fictional) — offers a GenAI-powered document classification service that reads scanned customs declarations and pre-sorts them by cargo category and risk tier before a human inspector reviews them.

**Proposed use:** Pre-triage of incoming customs declarations at GACWA's main port facility, reducing manual sorting time before Human-in-the-loop (HITL) inspection — the same HITL control required under Section 3 of [`ai-acceptable-use-policy.md`](ai-acceptable-use-policy.md).

**Data involved:** Scanned cargo manifests, shipper/consignee names, HS commodity codes, declared values. This is Non-Public Information (NPI) under GACWA's AI Acceptable Use Policy, which is precisely why this vendor requires a full assessment before onboarding rather than a same-day approval.

## 2. Data Handling Assessment (تقييم التعامل مع البيانات)

| Question | Vendor Response (as provided) | Assessor Note |
| --- | --- | --- |
| Where is data processed and stored? | Primary region: EU-West. Backup region: US-East. | Cross-border transfer of customs data to US-East requires a documented data transfer mechanism; flagged for legal review |
| Is customer data used to train the vendor's general-purpose models? | "Not by default; opt-out is available on Enterprise tier." | **Critical finding** — "not by default" means it happens unless explicitly disabled. Contract must contractually mandate opt-out, not rely on a configurable default |
| What is the data retention period after contract termination? | 90 days, then automated deletion | Acceptable; request written deletion certification at termination |
| Is data encrypted at rest and in transit? | AES-256 at rest, TLS 1.3 in transit | Meets baseline expectation |
| Does the vendor hold a current SOC 2 Type II report? | Yes, Security and Confidentiality categories only (no Availability) | Per Section 3 of the control mapping, this means uptime/DR claims in the SLA cannot be independently verified via the SOC 2 report alone — see Section 4 below |

## 3. Model Transparency Assessment (تقييم شفافية النموذج)

| Question | Vendor Response | Assessor Note |
| --- | --- | --- |
| Is the classification model a third-party foundation model, fine-tuned model, or proprietary model? | Fine-tuned third-party foundation model | Introduces a fourth party (the foundation model provider) into the supply chain — requires its own lightweight review under A.5.19/A.5.20 |
| Can the vendor explain why a given declaration was classified into a specific risk tier? | "Confidence score provided per classification; full feature attribution on Enterprise tier" | Confidence score alone is insufficient for an auditable customs decision — feature attribution should be a contract requirement, not an upsell |
| Has the model been evaluated for bias across shipper nationality, declared origin country, or commodity type? | No formal bias audit performed by vendor | **Gap** — recommend GACWA commission an independent bias evaluation before production use, given the discrimination risk of nationality/origin-correlated mis-triage |
| Does the vendor disclose model version changes that could alter classification behavior? | Change log published; no advance notice period specified | Contract should require minimum notice (recommend 30 days) before any model version change affecting production classification |

## 4. SLA Assessment (تقييم اتفاقية مستوى الخدمة)

| SLA Term | Vendor Offer | Assessor Note |
| --- | --- | --- |
| Uptime guarantee | 99.5% | Below GACWA's internal 99.9% threshold for systems in the customs clearance path; since Availability isn't in the vendor's SOC 2 scope (Section 2), this figure is contractual only, not independently attested |
| Incident notification window | Within 24 hours of vendor becoming aware | Too slow for a system feeding customs decisions; negotiate down to 4 hours, aligned with GACWA's own incident response tier for NPI-touching systems |
| Classification accuracy guarantee | "Best effort," no numeric commitment | Unacceptable as written — recommend a minimum precision/recall commitment on the risk-tier classification, with financial remedy for sustained misses |
| Support for HITL override / audit trail | Full override log retained 1 year | Meets requirement; confirm export format is compatible with GACWA's existing case management system |

## 5. Overall Risk Rating (التقييم الإجمالي للمخاطر)

Using the Likelihood × Impact scale from [`risk-register.md`](risk-register.md):

| Risk | Likelihood | Impact | Score | Rating |
| --- | --- | --- | --- | --- |
| NPI used for model training without explicit opt-out in contract | 3 | 5 | 15 | **High** |
| Unaudited model bias affecting risk-tier classification by shipper origin | 3 | 4 | 12 | **Medium** |
| Uptime below internal threshold with no independent Availability attestation | 3 | 3 | 9 | **Medium** |
| Undisclosed model changes altering classification without notice | 2 | 4 | 8 | **Medium** |

## 6. Recommendation (التوصية)

**Conditional approval.** ClearFlow AI may proceed to a limited pilot (non-production, shadow-mode classification only, no HITL decisions affected) contingent on:

1. Contractual mandatory opt-out from model training on GACWA data (not a configurable default).
2. Independent bias evaluation completed before any production use affecting risk-tier classification.
3. SLA renegotiation: 4-hour incident notification, minimum accuracy commitment, 30-day model-change notice.
4. Legal review of the EU-West/US-East cross-border data transfer mechanism.

This assessment gets re-run at contract renewal or upon any material change to the vendor's data handling, model, or SLA terms — a vendor risk assessment that isn't repeated on a cycle isn't governance, it's a one-time gate.
