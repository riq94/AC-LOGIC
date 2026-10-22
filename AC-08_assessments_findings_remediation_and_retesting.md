# AC-08 — Assessments, Findings, Remediation and Retesting

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Build a usable evidence-first manual assurance MVP with explicit results, real findings and independent verification.

**Prerequisites:** Approved standards, scope snapshots and evidence vault.

You are implementing **only Phase AC-08** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Implement assessment creation/submission/assignment with scoped requirements; controls start `not_tested` and have source/version/procedure/reviewer.
2. Implement verification states: not_tested, insufficient_evidence, pending_human_review, verified_pass, verified_fail, not_applicable (approved). Track risk_accepted separately; never translate it to pass.
3. Build a verified finding flow (hypothesis/tool_detected/human_confirmed/reproduced/false_positive/resolved_verified), severity rationale, CWE where appropriate, owner, due date and linked evidence.
4. Build remediation tasks, retest requests and independent reviewer actions with separation-of-duties; preserve earlier failures and evidence in history.
5. Implement notifications/audit and safe exports/links for issues; do not automatically close findings when a code change is detected.
6. Complete representative manual ASVS Level 2 / SSDF evidence review of a synthetic demo project as an end-to-end workflow.

### Required deliverables

Functional assessments UI; findings board; verification procedure entry; remediation/retest; audit trail; first truthful demo assessment and evidence report.

### Verification and security-negative tests

NT-01, NT-03, NT-11, NT-13, NT-14, NT-17; invalid statuses, self-approval, missing evidence/pass, failed control with accepted risk, change after report snapshot, concurrency.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Human assurance reviewer completes entire manual assessment/finding/retest cycle and demonstrates no unauthorized or AI-only verified pass. This is MVP core acceptance.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
