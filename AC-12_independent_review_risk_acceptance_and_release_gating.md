# AC-12 — Independent Review, Risk Acceptance and Release Gating

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Make verified review and human release decisions enforceable through state machines and policy, never a decorative approval button.

**Prerequisites:** Accepted findings, evidence, standards applicability, review assignments and role separation.

You are implementing **only Phase AC-12** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Implement reviewer assignment and conflicts-of-interest checks using authorship, remediation owner and role history. Block self-approval, including API, delegated role and concurrent approvals.
2. Define immutable decisions with scope, reviewer, outcome, reasons, evidence snapshot, time, identity/MFA context and signatures/attestations as designed.
3. Model risk acceptance separately from verification with policy-based eligible findings, owner, impact rationale, independent signoff, compensating controls, expiry and auto-invalidated status.
4. Implement server-side release gate engine using required applicable controls, evidence freshness, severity/policy blockers, approved review and operational checks. Produce BLOCK/REVIEW_REQUIRED/RECOMMEND_READY; final release authorization is human only.
5. Expose transparent breakdown of why release blocked; prevent weighted score from masking a single policy-blocking defect. Support controlled re-evaluation when evidence changes.
6. Record audit for rejected unauthorized approvals/overrides, retain past decisions and attach report snapshot.

### Required deliverables

Reviewer queue, assignment policies, COI verification, risk acceptance records, release gate engine, decision audit, exception expiry/reassessment, approval UX.

### Verification and security-negative tests

NT-03, NT-11–NT-14, NT-17; own code approved by same person, delegated role conflict, critical fail plus 99 passes, expired exception, stale evidence, approval race, missing MFA, report version changed.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Separate human assurance approver validates approval/audit evidence and proves blocking conditions cannot be bypassed via UI/API/worker. No autonomous release permission.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
