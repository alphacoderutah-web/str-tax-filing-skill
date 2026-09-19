---
id: source-of-truth-hierarchy
title: Source-of-truth hierarchy for filing decisions
category: concept
status: active
tags: [sources, verification, rates]
created: "2026-09-18T18:27:22"
updated: "2026-09-18T18:27:22"
---

<!-- compiled_truth -->
**Definition.** A fixed order of authority for every high-impact filing decision. When two sources conflict, the higher one wins and the conflict is logged.

The order, from resources/operating-rules.md:

1. The current live government portal.
2. Current official statute, rule, instructions, bulletin, FAQ or written agency communication.
3. Government registration or notice documents supplied by the operator.
4. Current filed-return and payment confirmations.
5. Current-period PMS exports.
6. Current-period marketplace tax and transaction reports.
7. Direct or manual booking records.
8. Payment-processor and accounting records.
9. Prior-period trackers and historical notes.
10. The operator's recollection.
11. General assumptions.

README.md gives a shorter version of the same order.

For choosing an account or certificate, SKILL.md uses a narrower four-step version: live portal record, then government documents, then a prior filed return or payment confirmation, then historical notes. A historical number that conflicts with a government document is replaced, and the correction is logged ([[verified-account-registry]]).

**Why it is this way.** Rules, rates, portal forms and marketplace behaviour change without notice, and sources based on memory had already proved wrong in practice. The hierarchy puts what the authority says for this period explicitly above what was true last period.

**Consequences recorded in the repository**

- Rates, due dates, marketplace treatment and form behaviour are verified from official sources every period (SKILL.md control 7). `resources/official-source-checks.md` lists what to verify and carries a last-reviewed date; it is not a set of permanent answers.
- A "current" form URL can serve the previous year's document, so check the year printed on it.
- For a tax the county administers, the county's own publication outranks a state summary table.
- Rates can change mid-year and mid-quarter. Verify against the period being filed, not against today.
- Filing frequency comes from the live account screen, not from operating memory. One jurisdiction's cadence says nothing about another's.
- Live portal labels override the written portal workflows.

**Boundaries.** The hierarchy decides which value to use. It doesn't authorise changing records: conflicts found during a run are logged, and registrations or mappings change only with the operator's explicit authorisation (SKILL.md control 6).


## Timeline

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "Created this page: Source-of-truth hierarchy for filing decisions"
  source: "resources/operating-rules.md; SKILL.md"
  affects: [source-of-truth-hierarchy]

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "captured from operating rules, SKILL.md account-number rule and learning log"
  source: "resources/operating-rules.md; SKILL.md; README.md; resources/learning-log.md"
  affects: [source-of-truth-hierarchy]
