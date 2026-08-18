# STR Tax Filing — a Claude Code skill

A tax-close controller for multi-property, multi-entity short-term rental businesses filing
across several jurisdictions and booking platforms.

It exists because this class of filing goes wrong in quiet, expensive ways: a property sitting in
the wrong management account, a marketplace that remits state tax but not county tax, a cancelled
booking that still owes tax, a "current" rate table that is a year out of date. The skill encodes
the controls that catch those before a return is submitted.

> **This repository ships as a template.** All government account numbers, entity names, property
> names, owner names and platform identifiers have been removed and replaced with placeholders.
> Populate `resources/account-registry.yaml` locally and keep your populated copy private — it
> contains live tax-account identifiers.

## Install

Copy this folder to `~/.claude/skills/str-tax-filing/`, then invoke it manually:

```
/str-tax-filing 2026-07 florida
```

Dry run — gather, calculate, reconcile and prepare the full packet, but submit nothing:

```
/str-tax-filing 2026-07 florida dry-run
```

## What it does

**Phase 0 — deadline and prior-risk check.** Resolves the period, reads each account's filing
frequency and due date from the portal, and flags accounts with prior penalty history for early
completion.

**Phase 1 — account matrix.** Builds `property → entity → platform account → jurisdiction → tax
type → government account → frequency` for every return in scope.

**Phases 2–4 — gather, normalise, reconcile.** Pulls booking-level data from every platform
account, separates guest stays from owner stays, cancellations and non-tax transactions, splits
charges into taxable and non-taxable components, determines which taxes each marketplace actually
remitted, and reconciles at booking, property, channel, tax-type and filing-account level.

**Phase 5 — Gate 1.** A consolidated pre-filing packet covering every account in scope: bases,
rates and their effective dates, marketplace exclusions by channel and tax type, allowances,
variances with classifications, and a confidence rating. Nothing is entered into a government
return until this is approved.

**Phase 6 — Gate 2.** At each portal's final review screen, exactly what the portal shows —
account, period, base, tax, allowance, fee, total debit, debit date — presented for approval
before any irreversible submit or pay.

**Phase 7 — archive and close.** Confirmations preserved immediately, payment status recorded as
scheduled versus cleared, unresolved issues carried forward.

## Design principles

**Two approval gates.** No figures enter a government return without approval of the packet; no
irreversible action happens without approval of the exact on-screen figures.

**A verified account registry.** Government account numbers live in one machine-readable file with
an explicit confidence tier and a live-verification flag. Values observed in a past cycle are the
lowest tier and are re-read from the portal before use.

**Source-of-truth hierarchy.** Live portal, then current official rules, then user-supplied
government documents, then filed returns, then platform exports, then prior-period notes, then
recollection. When sources conflict, the higher one wins and the conflict is logged.

**Secrets never persist.** No passwords, MFA codes, PINs, FEINs, bank routing or account numbers,
card numbers or login secrets in any skill file. Authentication and payment credentials are
entered by a human, in the browser.

**Manual invocation only.** `disable-model-invocation: true`, no broad pre-approved tool
permissions.

## Repository layout

| Path | Purpose |
|---|---|
| `SKILL.md` | The operating procedure — phases, gates, non-negotiable controls |
| `resources/account-registry.yaml` | **Template.** Government account registry |
| `resources/verified-tax-accounts.md` | **Template.** What to record per account and why |
| `resources/operating-rules.md` | Source hierarchy, identifier integrity, risk levels |
| `resources/property-account-map.md` | **Template.** Property → entity → account grouping logic |
| `resources/platform-account-map.md` | **Template.** Platform account → listing mapping |
| `resources/platform-data-protocol.md` | Booking-level fields needed for a normalised ledger |
| `resources/portal-workflows.md` | Per-portal filing procedure and controls |
| `resources/official-source-checks.md` | Which official sources to verify each period |
| `resources/learning-log.md` | Durable procedural lessons from real filing cycles |
| `templates/pre-filing-packet.md` | Gate 1 packet |
| `templates/close-summary.md` | Period close summary |

## Start here

`resources/learning-log.md` is the most transferable file in the repository — the accumulated
lessons from real cycles, with identifiers stripped. Most of them cost something to learn.

## Scope

Currently encodes Florida (state sales and use tax plus county tourist development tax) and Utah
(sales and use tax plus transient room tax). The phase structure, gates and controls are
jurisdiction-agnostic and extend to others.

## Licence

MIT — see `LICENSE`.

## A caveat worth stating

This encodes an operating procedure, not tax advice. Rates, rules, forms and portal behaviour
change without notice, and every control here assumes verification against current official
sources for the period being filed. Nothing in it substitutes for a qualified tax professional.
