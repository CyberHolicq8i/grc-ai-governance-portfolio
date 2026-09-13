# AI Incident Tabletop Exercise (تمرين محاكاة حادثة ذكاء اصطناعي)

*Global Air Cargo & Warehousing Authority — after-action writeup*

A tabletop exercise is only worth running if it produces decisions someone would actually have to make, under uncertainty, before all the facts are in. This document walks through a simulated AI incident affecting the ClearFlow AI classification tool introduced in [`third-party-ai-vendor-risk-assessment.md`](third-party-ai-vendor-risk-assessment.md), and the response it drives against [`ai-acceptable-use-policy.md`](ai-acceptable-use-policy.md) and the incident-handling controls mapped in [`soc2-iso27001-control-mapping.md`](soc2-iso27001-control-mapping.md).

## 1. Exercise Setup (إعداد التمرين)

| Field | Detail |
| --- | --- |
| **Exercise type** | Tabletop (discussion-based, no live systems affected) |
| **Scenario system** | ClearFlow AI customs-declaration classification tool (pilot, shadow-mode) |
| **Participants (role-played)** | Security Operations Center Lead, AI Governance Committee Chair, Warehouse Manager, Legal/Compliance Officer, Communications Lead |
| **Injects** | Delivered in three timed stages, each revealing new information before the group re-decides |

## 2. Inject 1 — T+0:00 (الحدث الأول)

**Scenario:** A Warehouse Manager notices that ClearFlow AI has classified an unusually high proportion of shipments from a specific country of origin as "high risk" over the past 48 hours — far above the historical baseline — triggering manual secondary inspections that are now backing up the warehouse floor.

**Facilitator question:** Is this a security incident, a model performance issue, or normal variance?

**Group decision:** Treated as a potential AI incident under Section 7.3 of the control mapping (equivalent to evaluating whether a security event "could or has resulted in a failure to meet objectives"), because a systematic classification skew by country of origin was flagged as a known risk category in the vendor's own risk assessment (Section 3, bias gap).

**Action taken:** SOC Lead pulls the classification tool into read-only audit mode; pilot remains in shadow-mode per its original scope, so no live customs decisions were affected. AI Governance Committee Chair is notified within the hour per internal escalation policy.

## 3. Inject 2 — T+2:00 (الحدث الثاني)

**New information:** Engineering confirms ClearFlow AI pushed a model version update six days ago. The vendor's change log documented it, but per the SLA gap identified in the vendor assessment, no advance notice was contractually required — so GACWA's team had no warning to watch for behavioral drift.

**Facilitator question:** Whose failure is this — GACWA's or the vendor's? Does that distinction change what happens next?

**Group decision:** Both, but differently. The vendor failed to provide adequate advance notice, which is now a contract renegotiation item, not just a lessons-learned note. GACWA's own gap was accepting a "best effort, no numeric accuracy commitment" SLA term in the pilot phase — the tabletop makes concrete what the vendor assessment flagged abstractly.

**Action taken:** Legal/Compliance Officer initiates a formal vendor incident report per the third-party risk process (A.5.19/A.5.20 in the control mapping). Communications Lead prepares an internal-only status note; because the pilot is shadow-mode and no customs decision was actually altered, no external disclosure obligation is triggered — the group explicitly confirms this determination rather than assuming it.

## 4. Inject 3 — T+6:00 (الحدث الثالث)

**New information:** A journalist reaches out to GACWA's public affairs office asking whether an "AI system" is "flagging shipments by nationality," having heard from an anonymous source inside the warehouse.

**Facilitator question:** How does the org respond, given the actual facts are more limited (a shadow-mode pilot with an unreviewed model update) than the framing in the inquiry ("flagging shipments by nationality")?

**Group decision:** Respond factually and narrowly: confirm a pilot tool is being evaluated in a non-production, human-reviewed capacity, that an anomaly was detected and is under review, and that no customs decisions have been made by the tool. Do not confirm or deny details of an ongoing vendor review. Escalate to legal before any statement goes out.

**Action taken:** Communications Lead and Legal/Compliance Officer jointly draft a two-sentence holding statement; AI Governance Committee Chair is looped in before release given the reputational and policy dimension.

## 5. Debrief — What Worked (ما نجح)

- **The shadow-mode pilot scope did its job.** Because the vendor assessment explicitly restricted ClearFlow AI to shadow-mode with no live HITL decisions affected, the actual operational and legal exposure of this incident was far lower than the media inquiry implied. This is the payoff of the "conditional approval, limited pilot" recommendation in the vendor assessment — it bought room to fail safely.
- **The escalation path was followed without improvisation.** SOC Lead → AI Governance Committee Chair happened inside the hour, matching the incident notification expectations set in Section 4 of the vendor assessment.

## 6. Debrief — Gaps Found (الثغرات المكتشفة)

| Gap | Fix |
| --- | --- |
| No contractual requirement for vendor to pre-notify model version changes | Add 30-day notice clause at next contract renegotiation (already recommended in the vendor assessment; this exercise is the evidence that the gap is not theoretical) |
| No internal monitoring baseline for classification-rate drift by category | Stand up automated drift alerting so a skew like this is caught by monitoring (A.8.16) rather than by a warehouse manager noticing a backlog |
| No pre-approved external holding statement template for AI-related media inquiries | Draft and pre-approve a template with Legal and Communications before the next pilot goes live |

## 7. Takeaway for the Portfolio

The value of a tabletop exercise isn't rehearsing the happy path — it's finding out, in a room with no real consequences, that "who tells the journalist what" was never actually decided in advance. Every gap in Section 6 is now a concrete action item with an owner, which is the difference between a tabletop exercise and a meeting where everyone agreed AI safety is important.
