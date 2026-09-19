---
slug: background
title: Project background
role: project background
updated: "2026-09-18T18:27:09"
---

# Project background

## Why

Short-term-rental tax filing across several entities, jurisdictions and booking platforms fails quietly. A property can sit in a different management account from the rest of its filing group. A marketplace can remit the state tax and not the local one. A cancelled booking can still owe tax. A rate table labelled "current" can be a year old. These mistakes show up later as underpayment, penalties or amendments.

This skill makes a Claude Code session act as a tax-close controller. It catches those failure modes before anything is submitted, and it hands every irreversible step back to a human.

Evidence: README.md (introduction and design principles), SKILL.md, resources/learning-log.md.

## Goals

- For a given filing period and scope, produce a reconciled filing packet for every government return in scope, traceable to booking-level source data. See [[booking-level-reconciliation]].
- Select the government account for every return from a verified registry, never from memory. See [[verified-account-registry]].
- Make no government filing or payment without two explicit human approvals. See [[two-approval-gates]].
- Close a period only when every in-scope account ends in a documented terminal state: filed and paid or scheduled, zero return filed, not due (documented), or blocked with an owner and a next action.
- Publish the procedure and the lessons from real filing cycles as a reusable template, without publishing any real identifiers. See [[public-template-sanitization]].

## Non-goals

- Tax advice. The README says the skill encodes an operating procedure and does not replace a qualified tax professional.
- Holding rates or rules as permanent truth. Rates, due dates, marketplace treatment and form behaviour are verified again from official sources every period. `resources/official-source-checks.md` lists what to verify; it is not a rate table. See [[source-of-truth-hierarchy]].
- Storing or typing credentials, MFA codes, CAPTCHAs or payment details. See [[safety-model]].
- Changing configuration during a filing run. PMS tax settings, tax-account registrations, property mappings and entity ownership are logged for a separate authorised task, never edited in the run.
- Running on its own. The skill is manual-invocation only.

## Target user

Operators (or their bookkeepers) of a short-term-rental business with several properties and entities, who:

- file state sales tax and local tourist or transient-room tax themselves,
- run more than one account per booking platform, and
- use Claude Code with a browser to work in government portals.

This is inferred from README.md and SKILL.md. The repository names no other audience.

## Scope and status

- **Jurisdictions encoded:** two US states, per the README scope section. Florida has state sales and use tax plus county tourist development tax. Utah has sales and use tax plus transient room tax. The README calls the phases, gates and controls jurisdiction-agnostic, but the portal workflows and official-source checks are specific to those two states.
- **Platform shape assumed:** two accounts each on one PMS and on two marketplaces (SKILL.md filing universe; resources/platform-account-map.md).
- **Status:** a public template at v2.1, published as a single initial commit on 2026-08-18. Release history is in CHANGELOG.md.
- **Provenance:** the procedure and the learning log came from real filing cycles, with identifiers stripped for publication (CHANGELOG.md v2.1; resources/learning-log.md).

## Open questions

- Will the repository be maintained through future filing cycles, with new learning-log entries and re-verified official sources? Or is it a one-time publication? The repository doesn't say.
- Are contributions invited? There is no CONTRIBUTING file or contribution guidance.
- Should the state-specific content move into a per-jurisdiction layer, so the template is jurisdiction-agnostic in its files as well as its structure? The README says the structure extends to other jurisdictions, but the files do not yet show how. The state-specific content is the filing universe in SKILL.md, the portal workflows and the official sources.
