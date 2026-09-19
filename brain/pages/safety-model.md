---
id: safety-model
title: "Safety model: manual invocation, no stored secrets, human-held credentials"
category: decision
status: active
tags: [security, credentials, invocation]
created: "2026-09-18T18:27:22"
updated: "2026-09-18T18:27:22"
---

<!-- compiled_truth -->
**Decision.** The skill runs only when a person invokes it, never holds secrets, and leaves every authentication and payment credential to a human in the browser.

- **Manual invocation only.** The SKILL.md frontmatter sets `disable-model-invocation: true`, and there is no broad `allowed-tools` pre-approval (CHANGELOG.md v2.0; README.md).
- **No secrets in any persistent file.** Skill files, notes, logs, worksheets and prompts never hold:
  - passwords, MFA or recovery codes, or PINs;
  - FEIN or SSN values;
  - bank routing or account numbers, or card numbers;
  - password-manager secrets;
  - login user IDs, unless one is operationally required.

  Only non-secret tax account identifiers and operational mappings are kept.
- **A human authenticates.** Claude opens the official login page and hands over for the password, MFA and CAPTCHA. It resumes once the authenticated account screen is visible. From there, Claude may navigate, select the verified account, enter non-secret figures, upload templates and review.
- **Irreversible actions need approval.** See [[two-approval-gates]].
- **No configuration changes during a run.** A filing run doesn't change PMS tax settings, tax-account registrations, property mappings or entity ownership. Issues are logged for a separate authorised task (SKILL.md controls 5 and 6).

**Why.**

- The source material used to build the skill contained credential-like and banking notes, which were deliberately left out (SKILL.md).
- The work moves real money to government accounts, so the model is designed to prevent both leaks and unattended action.
- Credentials are scoped per entity, so expect one authentication hand-off per entity per portal (resources/learning-log.md).

**Blast radius.**

- Every resource file repeats the exclusion list.
- The portal workflows open with the authentication protocol.
- The learning log must never receive secrets.

Related: [[public-template-sanitization]], [[verified-account-registry]].


## Timeline

- time: 2026-09-18T18:27:22
  kind: decision
  summary: "Created this page: Safety model: manual invocation, no stored secrets, human-held credentials"
  source: "CHANGELOG.md v2.0; SKILL.md"
  affects: [safety-model]

- time: 2026-09-18T18:27:22
  kind: decision
  summary: captured from SKILL.md security boundary and CHANGELOG safety model
  source: "SKILL.md; CHANGELOG.md; README.md; resources/portal-workflows.md; resources/learning-log.md"
  affects: [safety-model]
