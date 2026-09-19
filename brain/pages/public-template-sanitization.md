---
id: public-template-sanitization
title: "Publish as a sanitised template; populated data stays private"
category: decision
status: active
tags: [distribution, privacy, template]
created: "2026-09-18T18:27:22"
updated: "2026-09-18T18:27:22"
---

<!-- compiled_truth -->
**Decision.** The skill is published as a template. Every government account number, entity name, property name, owner name, street address and platform identifier was replaced with a placeholder. The four data files ship empty or with placeholders, to be populated locally and kept private (CHANGELOG.md v2.1; README.md).

**What ships as a template:**

- `resources/account-registry.yaml`
- `resources/verified-tax-accounts.md`
- `resources/property-account-map.md`
- `resources/platform-account-map.md`

Placeholders are angle-bracket tokens for the entity, property group, certificate and county account. Platform accounts get generic keys (`PMS-1`, `AIRBNB-1` and so on), marked `UNMAPPED`.

**What ships as real content:** the procedure (SKILL.md), the rules, the platform data protocol, the portal workflows, the official-source checks and the learning log. The lessons in the log have identifiers, entity and property names and amounts stripped. The README calls the learning log the most transferable file.

**What keeps real data out of Git:** only `.gitignore`. It excludes:

- local registry variants (`*.local.*`);
- the run directories: runs, source exports, confirmations, worksheets and packets;
- data file types: CSV, spreadsheets and PDF.

Its header says populated files must stay untracked, or the repository must stay private.

**Why.** The lessons and controls are useful to other short-term-rental operators with several entities, while the populated registry contains live tax-account identifiers (README.md). Keeping the private data layer apart from the procedure lets both exist. The reason for publishing is inferred from how the README frames the repository.

**Open questions (evidenced)**

- **Where a private registry goes.** SKILL.md always loads `resources/account-registry.yaml`, but the ignore rules cover `*.local.*` files, which SKILL.md never loads. If the tracked file is populated in place, as the README instructs, only discipline stops live identifiers reaching a commit. How a private registry should be wired in is unresolved.
- **Named jurisdictions and portals.** The public procedure still names the specific jurisdictions and portals the original business files in: the SKILL.md filing universe, `resources/portal-workflows.md` and `resources/official-source-checks.md`. These are public government sources, not account identifiers. Whether they belong in a generic template is a judgement the repository hasn't recorded.
- **No automated check.** Nothing scans for secrets or unfilled placeholders before a commit.

Related: [[safety-model]], [[verified-account-registry]].


## Timeline

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "Created this page: Publish as a sanitised template; populated data stays private"
  source: "CHANGELOG.md v2.1; README.md; .gitignore"
  affects: [public-template-sanitization]

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "captured from CHANGELOG v2.1, README template notice and .gitignore; open questions from SKILL.md load order"
  source: "CHANGELOG.md; README.md; .gitignore; SKILL.md"
  affects: [public-template-sanitization]
