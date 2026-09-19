---
id: verified-account-registry
title: Government accounts come from a verified registry with confidence tiers
category: decision
status: active
tags: [registry, identifiers, controls]
created: "2026-09-18T18:27:21"
updated: "2026-09-18T18:27:22"
---

<!-- compiled_truth -->
**Decision.** Government account and certificate numbers live in one machine-readable file, `resources/account-registry.yaml`. They are always read from there and confirmed against the live portal, never typed from memory.

Each entry carries:

- the entity and the property group it covers, plus jurisdiction, account type and filing forms where relevant;
- `evidence`: where the value came from;
- `confidence`, one of three tiers:
  - `VERIFIED_DOCUMENT`: read off a government registration or notice;
  - `VERIFIED_LIVE_PORTAL`: read off the authenticated account screen;
  - `HISTORICAL_PORTAL_OBSERVED`: seen in a past cycle, the lowest tier;
- `needs_live_verification`: must be cleared against the live portal before filing (Phase 1);
- optionally, a `correction` block that records a superseded value and why, so a known-wrong number can't quietly come back.

**Rules that go with it** (resources/operating-rules.md, "Identifier integrity"):

- Compare the account shown in the live portal with the registry before entering a return.
- Stop if the portal shows an unexpected account.
- Never merge two similar numbers, "fix" a digit by intuition, or combine digits from two sources.
- A portal label may name the entity rather than the property. The account number is the join, not the display name.

**Why.** The repository records two real failures (SKILL.md; resources/verified-tax-accounts.md; resources/learning-log.md):

- A certificate number in an older note had transposed digits.
- In one cycle, every county account number held in a registry was wrong, with no consistent pattern that could have corrected them.

That is why county accounts observed in the portal start in the lowest tier and are read again from the portal every period.

**Alternatives.** Keeping numbers in prose notes or prior-period trackers. That was the historical practice the corrections came from, and those sources now sit near the bottom of the [[source-of-truth-hierarchy]].

**Blast radius.**

- It feeds the Phase 1 matrix, the account-selection step of every portal workflow, and the "account verification source" field of the pre-filing packet.
- Once populated, the registry holds live identifiers, so it must stay private. See [[public-template-sanitization]].
- It holds account numbers only; credentials and banking data are excluded. See [[safety-model]].


## Timeline

- time: 2026-09-18T18:27:21
  kind: decision
  summary: "Created this page: Government accounts come from a verified registry with confidence tiers"
  source: "resources/account-registry.yaml; CHANGELOG.md v2.0"
  affects: [verified-account-registry]

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "captured from the registry template, operating rules and learning log"
  source: "resources/account-registry.yaml; resources/operating-rules.md; resources/verified-tax-accounts.md; resources/learning-log.md"
  affects: [verified-account-registry]
