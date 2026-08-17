# Policy Rewrite Exercise (تمرين إعادة صياغة السياسة)

A security policy is only as good as its enforceability. If a policy can't be violated in a way that's *detectable and actionable*, it isn't a policy — it's a suggestion. This exercise takes a vague draft and rewrites it against that standard.

## Original Draft (Vague & Unenforceable)

> "Warehouse staff and inspectors should try to keep their login details safe. Please do not use public AI tools to translate confidential shipping manifests. Passwords need to be strong."

**Why this fails as a policy, not just as writing:**

- *"should try to"* — no obligation, no violation condition. You can't fail an audit against "try."
- *"please do not"* — a request, not a rule. No stated consequence.
- *"strong"* — undefined. Strong by whose measure, checked how, enforced how?
- No mention of who verifies compliance, or what happens when someone doesn't.

## GRC Approved Policy (Enforceable Standard)

> **Section 3.1: Access Control and Acceptable Use**
>
> - **Mandatory (إلزامي):** All personnel **shall** utilize Multi-Factor Authentication (MFA) to access the cargo management network.
> - **Confidentiality (السرية):** Personnel **must not** upload, process, or translate any Non-Public Information (NPI), including shipping manifests or clearance documents, using unauthorized, publicly hosted GenAI platforms.
> - **Compliance Verification (التحقق من الامتثال):** Adherence to this policy is subject to automated Data Loss Prevention (DLP) monitoring and quarterly access audits (**تدقيق**). Violations will result in immediate suspension of network privileges.

## What actually changed, mechanically

| Weak pattern | Fixed by |
| --- | --- |
| "should try to" | "**shall**" / "**must not**" — modal verbs that create an obligation, not a preference |
| "strong" passwords, undefined | Replaced entirely with MFA — a control that's binary (on/off, verifiable) instead of a subjective adjective |
| "please do not use public AI tools" | Named the actual risk category (NPI exposure via unauthorized GenAI platforms) instead of naming a tool type — this is the AI Governance layer of the policy, and it's written to survive new tools showing up next year |
| No verification mechanism | Added DLP monitoring + quarterly audits — the policy states *how* compliance gets checked, not just what compliance looks like |
| No consequence | Named consequence (immediate suspension of network privileges) tied directly to the violation |

## Takeaway for the portfolio

The GRC skill being demonstrated here isn't "know the vocabulary" — it's converting good intentions into language that a DLP tool can monitor and an auditor can check a box against. That's the actual job.
