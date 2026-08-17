# Risk Assessment & Risk Register

*مستند تقييم المخاطر وسجل المخاطر*

## 1. The Core GRC Trinity (الثالوث الأساسي)

| Term | Arabic | Notes |
| --- | --- | --- |
| **GRC** — Governance, Risk, and Compliance | الحوكمة والمخاطر والامتثال | The umbrella discipline this whole repo sits under |
| **Risk Assessment** | تقييم المخاطر | The process: find risk, score it |
| **Risk Register** | سجل المخاطر | The artifact: where scored risk lives, gets tracked, gets owned |
| **Security Policy** | سياسة أمنية | The output: rules derived from what the register says matters |

The trinity only works in that order. A policy written before a risk assessment is just a guess dressed up as governance.

## 2. Risk Assessment Concepts (مفاهيم تقييم المخاطر)

Before mitigating a threat, an organization has to quantify its potential damage first — otherwise every risk "feels" equally urgent, and nothing gets prioritized. The standard formula this project uses:

> **Risk Level = Likelihood × Impact**

| Concept | Arabic | Definition |
| --- | --- | --- |
| **Asset** | أصل / أصول | The system, data, or physical item requiring protection |
| **Threat** | تهديد | The danger or bad actor attempting to compromise the asset |
| **Vulnerability** | ثغرة / نقطة ضعف | The weakness that lets the threat succeed |
| **Likelihood** | الاحتمالية | Probability of the event occurring (scale: 1–5) |
| **Impact** | الأثر | Severity of the damage if it occurs (scale: 1–5) |
| **Risk Level** | مستوى الخطر | The calculated score (Likelihood × Impact) |

**Reading the score:** with a 1–5 scale on both axes, the ceiling is 25. This project buckets it roughly as Low (≤6), Medium (7–14), High (15–19), Critical (20–25) — worth confirming against whatever matrix your organization actually adopts, since the bucket boundaries are a policy choice, not a law of nature.

## 3. Scenario Overview (نظرة عامة على السيناريو)

**Organization:** Global Air Cargo & Warehousing Authority
**Context:** Processes thousands of daily international shipments. IT infrastructure handles customs clearance data, dangerous goods manifests, and automated sorting systems.

This is the kind of organization where a risk register isn't academic — a scored "15" on the wrong asset is a grounded shipment or a customs violation, not just a red cell in a spreadsheet.

## 4. Risk Register (سجل المخاطر)

The Risk Register is the centralized tracking document used to log vulnerabilities, assess their initial danger (**Inherent Risk** — الخطر الكامن), and assign controls to reduce the danger (**Residual Risk** — الخطر المتبقي).

| Risk ID | Asset (الأصول) | Threat & Vulnerability (التهديد والثغرة) | Likelihood | Impact | Inherent Risk Score | Mitigation Control (ضابط رقابي) | Residual Risk | Risk Owner (مالك الخطر) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **RSK-01** | Air Cargo Clearance Database | **Threat:** Ransomware attack.<br>**Vulnerability:** Unpatched server software. | 3 | 5 | **15 (High)** | Implement automated weekly patching and immutable offline backups. | Low (3) | IT Infrastructure Lead |
| **RSK-02** | Inspector Tablets | **Threat:** Unauthorized access to manifests.<br>**Vulnerability:** Tablets lack screen locks. | 4 | 4 | **16 (High)** | Enforce Mobile Device Management (MDM) with biometric authentication and 30-second auto-lock. | Low (4) | Security Operations Center |
| **RSK-03** | Warehouse Smart Scanners | **Threat:** Data manipulation.<br>**Vulnerability:** Default vendor passwords still active. | 4 | 5 | **20 (Critical)** | Mandate password rotation prior to deployment on the production network. | Low (5) | Warehouse Manager |

### Reading this register

- **RSK-03 is the one that should keep you up at night.** Default vendor credentials on a production asset is one of the oldest, laziest, and still most common breach vectors — it scores Critical for a reason, and the fix (mandatory rotation before deployment) is cheap relative to the exposure it closes.
- **Inherent vs. Residual is the whole point of the register.** RSK-02 goes from 16 (High) to 4 (Low) purely because of one control — MDM enforcement. That delta is the register earning its keep: it's evidence a specific control did specific work, not a vague "we take security seriously."
- **Every row has an owner.** A risk without an owner isn't tracked, it's just noted. The Risk Owner column is what turns this from a document into an accountability structure.

## Glossary quick-reference

| EN | AR |
| --- | --- |
| Inherent Risk | الخطر الكامن |
| Residual Risk | الخطر المتبقي |
| Mitigation Control | ضابط رقابي |
| Risk Owner | مالك الخطر |
