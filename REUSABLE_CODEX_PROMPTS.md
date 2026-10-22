# Reusable CODEX operational prompts

Use these after installing repository `AGENTS.md`. Paste one template and replace square-bracket placeholders. These are operational prompts, not approval signatures.

## Prompt R-01 — Read-only repository orientation

```text
Perform READ-ONLY discovery for AC Logic before implementing [PHASE/TASK]. Read AGENTS.md, 00_MASTER_DIRECTIVE.md, the active phase file, relevant reference policies, and any accepted ADRs. Inventory existing packages, APIs, database, migrations, tests, permissions, CI and deployments. Describe inconsistencies, risks, exact proposed file changes, negative tests, rollback effects and approvals required. Do not write files, install dependencies, change credentials or deploy. Produce a phase implementation plan and stop for approval.
```

## Prompt R-02 — Execute an approved phase

```text
Execute only AC Logic [PHASE ID: TITLE] under the approved plan [PLAN REFERENCE]. Re-read AGENTS.md and the phase specification. Preserve earlier completed gates. Implement a minimal, real vertical slice without weakening authorization, RLS, evidence integrity or reviewer independence. Add the specified positive and negative tests; document migrations and rollback. Run available checks and report exact outcomes. Do not touch production, perform external scans, grant permissions, create GitHub writes or merge/deploy without separate explicit authority. Stop at the human acceptance gate with evidence and unresolved risks.
```

## Prompt R-03 — Independent technical review (separate session / human reviewer)

```text
Act as a skeptical independent technical reviewer of [PHASE/PR/COMMIT]. Do not trust implementation summaries; inspect code, migrations, tests and CI evidence. Evaluate architecture consistency; threat boundaries; tenant/RLS/auth and storage; API security; data constraints; worker/AI trust boundaries; standards accuracy; reviewer independence; logging/privacy; rollback. Try to identify missing negative tests and ungrounded pass claims. Report findings with path:line, severity, reproduction reasoning, affected tenants and suggested tests. Distinguish proven defects from hypotheses. Do not sign the final review as a human.
```

## Prompt R-04 — Security remediation

```text
Remediate only accepted findings [IDS] against [COMMIT]. First confirm reproduction and affected scope, describe minimal design, tests and rollback, then implement after approval. Add regression/negative tests, run them and compare before/after evidence. Keep existing finding history and verified facts; do not close findings until an independent verifier accepts the retest evidence. Produce a concise remediation handoff.
```

## Prompt R-05 — Phase verification & evidence collection

```text
Verify [PHASE] against its checklist. Identify exact tests available in repository and execute only authorized local/staging checks. Collect sanitized command output, commits, migration version, scan versions and coverage. Classify each acceptance criterion PASS/FAIL/NOT RUN/NOT APPLICABLE (with rationale). Do not transform skipped tests into passes; do not claim release approval. Identify blockers and create a human approval request.
```

## Prompt R-06 — Release readiness

```text
Perform a READ-ONLY release gate review for candidate [RELEASE/COMMIT]. Compare required AC Logic reference/ACCEPTANCE_GATES.md policies against evidence, tenant isolation tests, reviewer signoffs, critical findings, stale scans, standards versions, migration/recovery status, monitoring and data processing/license review. Output BLOCK, REVIEW REQUIRED or RECOMMEND READY with rationale, unresolved risks, evidence IDs and approver list. Do not deploy or self-approve.
```

## Prompt R-07 — End-of-phase handoff

```text
Prepare AC Logic phase [PHASE] handoff: completed scope, deferred scope, changed paths, ADR/migration/API changes, tests and actual results, secrets/config changes (names only), unresolved risks, risk owner, rollbacks, evidence links and precise next-phase prerequisites. Summarize approval still needed. Do not infer success from absence of errors.
```
