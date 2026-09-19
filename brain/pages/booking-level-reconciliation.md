---
id: booking-level-reconciliation
title: Booking-level reconciliation before filing
category: concept
status: active
tags: [reconciliation, marketplace, ledger]
created: "2026-09-18T18:27:22"
updated: "2026-09-18T18:27:22"
---

<!-- compiled_truth -->
**Definition.** Every return is built from one normalised, booking-level ledger and reconciled before anything is filed (SKILL.md control 1). When charge mappings are suspect, tax collected never stands in for a verified taxable base (control 4).

**The ledger** (resources/platform-data-protocol.md). Guest stays, owner stays, cancellations and refunds, and non-tax transactions are separated first. Source exports are kept unmodified. Then each booking gets:

- its property, entity, jurisdiction, platform account, channel and filing period;
- its charges split into rent, cleaning, pet fees, other required fees, and optional charges or deposits;
- separate state and local taxable bases;
- evidence of any marketplace remittance of state and local tax;
- tax collected by the business, expected tax, variance, and the evidence source.

**Levels.** Reconciliation runs at five levels: booking, property, channel, tax type and filing account. It compares:

- the PMS base, marketplace evidence and direct records;
- tax collected by each platform and by the business;
- expected tax at verified rates;
- the portal's own calculation.

**Marketplace channel matrix.** For each jurisdiction and tax type, a per-period matrix records, with evidence, whether each channel collected and remitted the tax and whether the business must report it. No row is marked marketplace-remitted without current evidence.

- Two marketplaces in one jurisdiction can take opposite positions.
- A marketplace remitting state tax does not mean it remits local tax (resources/operating-rules.md; resources/learning-log.md).
- The learning log describes a ratio test that proves which taxes a platform remits when its report has no breakdown by tax type.

**Variance classes.** Every variance gets one of five classes:

- explained and documented;
- open and unexplained;
- material and high-risk;
- immaterial and noted;
- needs government or CPA verification.

Amounts are reconciled to the cent, and differences are never rounded away.

**Known traps it is built to catch** (resources/learning-log.md; resources/property-account-map.md):

- A property in a different PMS account from the rest of its filing group. A return built from one account then comes out short.
- One physical property split into two PMS records by channel.
- Cancel-and-rebook pairs that count the same revenue twice.
- Cancelled bookings with a retained, unrefunded charge, which are taxable but carry no tax in the PMS.
- Marketplace reports on a payout basis against a PMS ledger on an arrival or accrual basis. Explain the timing variance booking by booking; whatever remains is a real difference in the base.
- PMS report options that hide zero-tax bookings by default.
- Taxable-charge columns that exceed the base actually taxed.
- Duplicate tax lines for the same tax.

**Boundary.** When expected tax differs from what the PMS collected, the run files what current rules require and logs the over- or under-collection. It leaves PMS tax settings alone, and a separate authorised audit follows ([[safety-model]]).

The reconciled result feeds the Gate 1 packet ([[two-approval-gates]]). Rates and treatment come from the [[source-of-truth-hierarchy]].


## Timeline

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "Created this page: Booking-level reconciliation before filing"
  source: "SKILL.md phases 3-4; resources/platform-data-protocol.md"
  affects: [booking-level-reconciliation]

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "captured from SKILL.md phases 3-4, platform data protocol, operating rules and learning log"
  source: "SKILL.md; resources/platform-data-protocol.md; resources/operating-rules.md; resources/property-account-map.md; resources/learning-log.md"
  affects: [booking-level-reconciliation]
