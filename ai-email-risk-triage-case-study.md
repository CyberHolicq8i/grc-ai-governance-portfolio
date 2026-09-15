# AI-Assisted Email Risk Triage: A Personal Case Study

*Study note / mini-project by Ahmad Almutawa — Customs & Compliance Inspector, transitioning into Cybersecurity GRC & AI Governance.*

## Why I did this

Most GRC and phishing-awareness material talks about email risk in the abstract. I wanted a first-hand exercise: point an AI agent (Claude, via a browser-automation session) at my own real inbox, have it triage what was there against a simple risk taxonomy, and see what it actually found — including where *I* would have jumped to the wrong conclusion.

**Note on data:** every example below is generalized or anonymized. No real personal identifiers, order numbers, account details, or message contents are reproduced.

## Method

1. Scope: recent mail across the Junk folder and the primary/"Other" inbox split (roughly a three-week window, ~250 messages).
2. Triage taxonomy: for each message, classify as (a) already correctly filtered, (b) legitimate marketing/transactional, (c) legitimate but security-relevant (account alerts, billing notices), or (d) suspected phishing/scam.
3. For anything landing in category (d), or anything that merely *looked* alarming, verify before acting:
   - Read the real sender address, not just the display name.
      - Inspect the actual hyperlink targets in the message body (via DOM inspection, not by clicking them) rather than trusting the visible link text or "Update Now" button styling.
         - Cross-check the claimed context (e.g., "this is a copy of an alert sent elsewhere") against known account configuration (e.g., a configured recovery email) before treating it as spoofed.
         4. Only messages that fail verification get escalated (e.g., via a mail provider's "Report Phishing" action). Nothing gets flagged on appearance alone.

         ## What the taxonomy actually found

         | Category | Share of sample (approx.) | Typical risk |
         |---|---|---|
         | Correctly auto-filtered marketing/spam | ~55% | Low |
         | Legitimate transactional receipts (delivery, ride-hailing, travel, BNPL) | ~25% | None |
         | Legitimate but security-relevant (subscription billing issues, account sign-in alerts) | ~15% | None once verified |
         | Confirmed phishing/scam | 0% | — |

         Zero confirmed phishing in this sample is itself a data point worth sitting with — it's tempting to assume "no hits" means "nothing to learn," but the more interesting result was in the near-misses.

         ## The interesting part: two false-positive scares

         **Case 1 — the "subscription billing problem" pattern.** Several near-identical emails arrived claiming a payment method had failed for a handful of unrelated paid subscriptions (a video-streaming service, a couple of AI-coding tools, a cloud AI service). Same template, generic greeting, urgent-sounding subject line, a prominent "Update Payment Information" button. This is *exactly* the shape of a classic App-Store-style phishing kit — impersonate the platform, create urgency around losing access, harvest card details on a fake page.

         On inspection: the sender address resolved to the platform's real bulk-mail domain, and — critically — every link in the message, extracted directly from the HTML rather than by hovering or clicking, pointed to the platform's actual account-management domains. These were genuine billing notices; the "scam-shaped" template is simply what the platform's real transactional email looks like. Lesson: *template similarity to a phishing kit is not evidence of phishing — link destination is.*

         **Case 2 — the "security alert" that looked forwarded/spoofed.** An email claimed to be "a copy of a security alert" sent to a different address, referencing a linked third-party app being granted account access. On its face this fits a common spoofing pattern (name-drop a real account to build credibility). On inspection, the sender domain was the real security-notification domain of a major account provider, and the "copy sent to a recovery address" framing matched an actual, previously-configured recovery-email relationship on the account. Lesson: *don't assume a message referencing account configuration is fabricated — check whether the configuration it describes is actually true first.*

         ## Risk register (template)

         | ID | Signal observed | Initial risk read | Verification step | Final classification | Action |
         |---|---|---|---|---|---|
         | 1 | Urgent billing-failure email, generic greeting, CTA button | Medium-High (phishing-shaped) | Extracted real link hostnames from message DOM | Legitimate | No action; user follow-up on actual payment method |
         | 2 | "Copy of a security alert" referencing another account | Medium (spoofing-shaped) | Confirmed sender domain + confirmed recovery-email configuration | Legitimate | No action; user confirmed OAuth grant was expected |
         | 3 | High-volume retail/marketing senders | Low | Sender reputation, no credential/payment ask | Legitimate marketing | Left to existing spam filter |

         ## Takeaways for GRC / security-awareness practice

         - A risk register is only as good as its verification step — "looks suspicious" and "is malicious" are different rows in the table, and collapsing them either over-alerts (fatigue) or under-alerts (missed real threats).
         - Automating the *triage* (volume sorting, first-pass categorization) freed up attention for the *verification* work that actually needs judgment — which is where an analyst's time is best spent.
         - For anyone building their own version of this: check sender domains and real link destinations, not visual polish or urgency language alone — well-produced phishing and well-produced legitimate billing email can look identical at a glance.

         ## Tools used

         Claude (Anthropic) with browser automation, used to enumerate inbox contents, extract sender headers, and pull real hyperlink targets from message HTML for verification, cross-referenced manually before drawing conclusions above.

         ---
         *Part of my ongoing cybersecurity GRC / AI governance study notes. Feedback welcome.*
