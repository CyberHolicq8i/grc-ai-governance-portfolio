# AI Acceptable Use Policy (سياسة الاستخدام المقبول للذكاء الاصطناعي)

*Fictional organization: Global Air Cargo & Warehousing Authority*

A policy that says "use AI responsibly" isn't a policy — it's a slogan. This document exists to name exactly which AI uses are permitted, which are prohibited, and how compliance is checked, following the same enforceability standard applied in [`policy-rewrite.md`](policy-rewrite.md).

## 1. Purpose and Scope (الغرض والنطاق)

This policy governs the use of any Artificial Intelligence (AI) or Generative AI (GenAI) tool — public, vendor-supplied, or internally hosted — by any employee, contractor, or inspector of the Global Air Cargo & Warehousing Authority (GACWA) in the course of their duties. It applies whether the tool is accessed on a corporate device, a personal device used for work, or embedded inside a third-party vendor product (see [`third-party-ai-vendor-risk-assessment.md`](third-party-ai-vendor-risk-assessment.md) for how those vendor tools get vetted before this policy ever applies to them).

## 2. Definitions (تعريفات)

| Term | Arabic | Definition |
| --- | --- | --- |
| **Approved AI Tool** | أداة ذكاء اصطناعي معتمدة | A GenAI system that has completed GACWA's vendor risk review and is listed in the internal AI Tool Registry |
| **Non-Public Information (NPI)** | معلومات غير عامة | Any cargo manifest, customs clearance record, personnel data, or system credential not intended for public release |
| **Shadow AI** | ذكاء اصطناعي غير مصرح به | Any AI tool in active use by staff that has not gone through the Approved AI Tool review process |
| **Human-in-the-loop (HITL)** | إشراف بشري | A control requiring a qualified human to review and approve AI output before it is acted upon |

## 3. Permitted Use (الاستخدام المسموح)

Employees **may** use an Approved AI Tool to:

- Draft or summarize internal, non-sensitive correspondence.
- Generate first-draft code, scripts, or documentation that will undergo human review before deployment.
- Translate publicly releasable material (press releases, public-facing signage, training materials that contain no NPI).

All AI-assisted output used in an operational, legal, or customs-facing decision **shall** be reviewed under Human-in-the-loop (HITL) controls before action is taken — an AI tool may draft a risk flag; it does not get to close one.

## 4. Prohibited Use (الاستخدام المحظور)

Personnel **must not**:

- Upload, paste, or otherwise process any Non-Public Information — including cargo manifests, dangerous-goods declarations, customs clearance data, or inspector notes — into any AI tool that is not on the Approved AI Tool Registry. This includes public consumer chatbots accessed through a personal account.
- Use an AI tool's output as the sole basis for a customs clearance, cargo release, or security-flag decision without HITL review.
- Connect any AI tool, plugin, or browser extension to GACWA systems via an unreviewed API key or OAuth grant.
- Use Shadow AI tools to perform any task that touches NPI, regardless of convenience or perceived time savings.

## 5. Approval Process for New AI Tools (عملية اعتماد أدوات جديدة)

1. Requestor submits the tool name, vendor, and intended use case to the AI Governance Committee.
2. The vendor undergoes the standard third-party risk review (data handling, model transparency, SLA terms).
3. A Data Protection Impact Assessment (DPIA) is completed if the tool will process any personal or NPI data.
4. Approved tools are added to the AI Tool Registry with a defined scope of permitted use; the registry is reviewed quarterly.

## 6. Compliance Verification (التحقق من الامتثال)

- **Monitoring:** Data Loss Prevention (DLP) rules flag any attempt to transmit NPI-pattern data (manifest IDs, container numbers, personnel IDs) to a non-approved external domain.
- **Audit:** Quarterly access and usage audits (تدقيق) cross-reference AI Tool Registry entries against network egress logs.
- **Attestation:** All personnel with system access complete an annual acknowledgment of this policy.

## 7. Violations and Consequences (المخالفات والعواقب)

| Violation | Consequence |
| --- | --- |
| First unintentional use of an unapproved AI tool with no NPI exposure | Documented warning and mandatory retraining |
| Use of Shadow AI resulting in NPI exposure | Immediate suspension of network privileges pending investigation |
| Acting on unreviewed AI output to clear or flag cargo | Immediate suspension of network privileges and referral to the AI Governance Committee |

## 8. Ownership and Review

This policy is owned by the AI Governance Committee and is reviewed annually or upon the introduction of any new AI capability into GACWA's operating environment.

## Why this document belongs in the portfolio

An acceptable-use policy is the artifact that turns "we're thoughtful about AI" into something an auditor can actually check: named approval process, named monitoring mechanism, named consequence. The permitted/prohibited split above is deliberately concrete — an inspector reading Section 4 should know, without needing to ask, whether pasting a manifest into a public chatbot to get a quick translation is against the rules. It is.
