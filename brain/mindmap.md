---
slug: mindmap
title: Feature mindmap
role: feature mindmap
updated: "2026-09-18T18:27:09"
---

# Feature mindmap

## Feature mindmap

```mermaid
mindmap
  root((STR tax filing skill))
    Controls
      Twelve non-negotiable controls
      Gate 1 packet approval
      Gate 2 on-screen approval
      Completion standard
      Dry-run mode
    Account registry
      Confidence tiers
      Live-verification flag
      Recorded corrections
      Identifier integrity
    Source data
      PMS exports
      Marketplace tax reports
      Direct bookings
      Normalised booking ledger
    Reconciliation
      Booking to filing-account levels
      Marketplace channel matrix
      Timing-basis variance
      Variance classes
      Cancelled-booking checks
    Portal execution
      Human authentication hand-off
      Per-portal workflows
      Template-upload returns
      Error recovery
    Deadlines and risk
      Live filing frequency
      Penalty-history accounts filed early
      Risk levels
    Close and archive
      Confirmations saved at once
      Scheduled vs cleared
      Close summary
    Knowledge
      Learning log
      Official source checks
    Distribution
      Public template
      Placeholders
      Git-ignored run data
      MIT licence
```

## Where each branch is explained

- Controls and gates: [[two-approval-gates]], [[safety-model]]
- Account registry: [[verified-account-registry]]
- Source data and reconciliation: [[booking-level-reconciliation]]
- Rates, rules and which source wins: [[source-of-truth-hierarchy]]
- Distribution: [[public-template-sanitization]]
