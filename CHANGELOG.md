# Changelog

## v2.1 — public template release

Sanitised for public distribution. All government account numbers, entity names, property names,
owner names, street addresses and platform identifiers removed and replaced with placeholders.
`account-registry.yaml`, `verified-tax-accounts.md`, `property-account-map.md` and
`platform-account-map.md` now ship as templates to populate locally.

### Added from a full live filing cycle

Ten returns filed across two states, three entities and two counties, plus a second-state
verification pass. Lessons captured in `resources/learning-log.md`:

- **Identifier integrity** — historical county account numbers proved wrong in a real cycle;
  live-portal values are authoritative and must be re-read every period.
- **Credential scoping** — state guest-filing identifiers are per-entity; county portals may need
  a separate login per entity. A missing account is usually a credentials-scope issue, not a
  closed account.
- **Rate sourcing** — a "current" form URL can serve the prior year; for a county-administered
  tax the county overrides the state's summary table.
- **Marketplace posture** — two platforms in one jurisdiction can have opposite postures. Added
  the ratio test for proving which taxes a platform actually remits without a tax-type breakdown.
- **Cancelled bookings** — the cancel-and-rebook double-count, and the taxable retained charge a
  PMS records with zero tax.
- **Template-upload filings** — write literal values not formulas, carry full precision, preserve
  workbook structure, verify the row's account before writing to it, check the required file
  format.
- **Portal behaviour** — verify status before re-filing after an error; a login URL may serve an
  authenticated view of a different account; submission logs can be profile-scoped so another
  user's work is invisible.
- **Fees and allowances** — allowance caps, e-file/e-pay conditionality, and convenience fees that
  vary by portal and method.
- **Cadence** — one jurisdiction's monthly close does not imply another's quarterly account is
  due; a "processed" period can still carry a pending amendment.

## v2.0

### Structure

- Machine-readable government account registry with explicit confidence tiers and a
  live-verification flag.
- Separate live-verification status for county account numbers observed in prior cycles.
- Two approval gates before any irreversible filing or payment action.
- Zero-return and rate-verification controls.
- Prior penalty-waiver history converted into deadline risk controls.
- Platform account-mapping framework for multiple accounts per platform.
- Explicit exclusion of banking, FEIN, PIN and credential-like data from all persistent files.
- Utah form routing: TC-62M / TC-62S for sales and use, TC-62T for transient room.

### Safety model

- Manual-only invocation (`disable-model-invocation: true`).
- No broad `allowed-tools` pre-approval.
- Human handles authentication, MFA, CAPTCHA and payment credentials.
- Current official source and live portal override historical notes.
