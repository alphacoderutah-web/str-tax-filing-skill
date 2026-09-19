---
slug: flow
title: Key flows
role: key flows
updated: "2026-09-18T18:27:09"
---

# Key flows

## End-to-end path of a typical request

A filing run covers one period and one scope, for example one month for one state or one quarter for all states. With `dry-run`, the run stops after Gate 1, and nothing is submitted or changed.

```mermaid
sequenceDiagram
  participant O as Operator
  participant C as Claude running the skill
  participant R as Registry and rules
  participant P as PMS and marketplaces
  participant G as Government portal
  O->>C: Invoke with period, scope, optional dry-run
  C->>R: Load resources in fixed order
  C->>G: Phase 0 - read frequency, due date, open period
  C->>C: Flag penalty-history accounts and deadlines within 3 business days
  C->>R: Phase 1 - build the account matrix
  C->>G: Verify entries flagged needs_live_verification
  C->>P: Phase 2 - export reports from every platform account
  C->>C: Phase 3 - normalise into a booking-level ledger
  C->>C: Phase 4 - reconcile and classify every variance
  C->>O: Phase 5 - consolidated pre-filing packet (Gate 1)
  O-->>C: Explicit approval (dry-run ends here)
  C->>G: Phase 6 - open the official login page
  O->>G: Enter credentials, MFA, CAPTCHA
  C->>G: Select the account, confirm it against the registry, enter figures
  G-->>C: Portal-calculated totals
  C->>C: Stop if the portal total differs from the packet
  C->>O: Final review screen exactly as shown (Gate 2)
  O-->>C: Explicit approval of those figures
  C->>G: Submit and pay
  G-->>C: Confirmation and reference
  C->>C: Phase 7 - archive confirmations, record scheduled vs cleared
  C->>O: Close summary with a terminal state per account
```

The Phase 1 account matrix maps property, entity, platform account, jurisdiction, tax type, government account and filing frequency.

## Other important flows

- **Account mismatch at entry.** If the portal shows an account number that doesn't match the registry, the run stops. The mapping is resolved before any figures are entered. See [[verified-account-registry]].
- **Portal error mid-filing.** After any portal error, check the status of the return or row before filing again; never re-submit blind. Before handing over for authentication, confirm which account the session is actually signed into (resources/learning-log.md, "Portal behaviour").
- **Filing by template upload.** Some returns are filed by uploading the authority's own spreadsheet. The rules (resources/learning-log.md; resources/portal-workflows.md):
  - write literal values, not formulas, at full precision;
  - keep the workbook structure unchanged;
  - verify each row's account before writing to it;
  - use the required file format.

  A missing property row stops the upload path.
- **PMS tax mismatch.** When expected tax differs from what the PMS collected, the run:
  1. keeps the verified base;
  2. files what current rules require;
  3. logs the over- or under-collection;
  4. opens a separate authorised audit after filing.

  Tax settings are never changed during the run. See [[booking-level-reconciliation]].
- **Separate filing and payment.** Where filing and payment are separate irreversible actions, each needs its own Gate 2 approval, unless both were listed and approved together. See [[two-approval-gates]].
- **Close.** Each account must end in one of four states:
  - filed and paid or scheduled, confirmed;
  - zero return filed, confirmed;
  - not due, documented;
  - blocked, with an owner and a next action.

  A period is closed only when every in-scope account is. Unresolved issues carry forward to the next run.
- **Learning capture.** Phase 7 adds to resources/learning-log.md only durable, verified procedural facts or mappings the operator confirmed, and never secrets.
