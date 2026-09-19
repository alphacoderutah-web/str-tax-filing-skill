---
id: two-approval-gates
title: Two approval gates before any filing or payment
category: decision
status: active
tags: [controls, approval, gates]
created: "2026-09-18T18:27:21"
updated: "2026-09-18T18:27:21"
---

<!-- compiled_truth -->
**Decision.** No government filing or payment happens without two separate, explicit human approvals.

- **Gate 1: the filing packet.** Before any final figure goes into a government return, Claude presents one consolidated packet covering every account in scope. It is built from `templates/pre-filing-packet.md`, one packet per return plus a consolidated summary. It shows:
  - period, jurisdiction and tax type, entity, government account, properties and platform sources;
  - gross receipts and taxable base;
  - marketplace-remitted base by channel and tax type, and the business-remitted base;
  - rates with their effective dates;
  - tax, allowance, penalty and interest, expected payment and known fees;
  - variances with explanations, a confidence rating and open issues.
- **Gate 2: the irreversible action.** At each portal's final review screen, Claude presents exactly what the portal shows: account, period, base, tax, allowance, penalty, fee, total debit, debit date and masked payment method. It clicks nothing irreversible (submit, file, pay, authorise) until the operator approves those figures. When filing and payment are separate irreversible actions, each needs approval, unless both were listed and approved together.
- **Between the gates:** if a portal total differs from the packet, the run stops for reconciliation (SKILL.md control 12).
- **`dry-run`** runs everything up to and including the Gate 1 packet, and changes nothing.

**Why.** Filing and payment can't be undone and are audit-relevant. Card and e-check payments are often non-cancellable once made (resources/learning-log.md). The two gates approve different things:

- Gate 1 approves the numbers the business believes are right.
- Gate 2 approves what the government system will actually record and debit. That can differ through portal rounding, allowance computation, fees or a wrongly selected account.

Keeping them separate catches both preparation errors and entry errors. SKILL.md and README.md state the gates; this reasoning about why there are two is partly inferred.

**Alternatives.** The repository doesn't discuss any. A single approval at either point, or unattended submission, would lose one of the two checks (inferred).

**Blast radius.**

- Every portal workflow ends with "Stop at Gate 2".
- The pre-filing packet template has a Gate 1 status field.
- The completion standard relies on the confirmations collected after Gate 2.

Related: [[safety-model]], [[booking-level-reconciliation]].


## Timeline

- time: 2026-09-18T18:27:21
  kind: decision
  summary: "Created this page: Two approval gates before any filing or payment"
  source: "SKILL.md; README.md"
  affects: [two-approval-gates]

- time: 2026-09-18T18:27:21
  kind: decision
  summary: captured from SKILL.md approval gates and README design principles
  source: "SKILL.md; README.md; resources/learning-log.md"
  affects: [two-approval-gates]
