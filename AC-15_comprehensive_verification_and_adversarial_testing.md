# AC-15 — Comprehensive Verification and Adversarial Testing

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Challenge assumptions with adversarial, negative, integration, reliability and privacy tests and fix all release-blocking faults.

**Prerequisites:** Mature enough product integration for meaningful staging tests; test authority limited to synthetic owned environments.

You are implementing **only Phase AC-15** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Execute reference/TEST_AND_THREAT_MATRIX.md in an isolated authorized staging environment, record case-to-control-to-evidence mapping; create missing fixtures.
2. Run focused SAST, dependency/secret and misconfiguration analysis, integration/E2E/RLS/storage tests, multi-tenant property tests and approval-state tests.
3. Exercise poisoned repository/prompt, webhook replay, invalid JWT/role spoof, forbidden GitHub installation, malicious upload, sandbox escape attempts (within controlled safe lab), SSRF and queue/backup failure.
4. Verify all issued report and audit statements have evidence; replay historically imported standards versions and assessment snapshots.
5. Validate accessibility, performance under tenant limits, pagination, 500/error behavior, retention, deletion and no code/secret leakage to logs or model when not allowed.
6. Create independent security findings and remediation backlog with reproduction, severity and scope; retest after fixes.
7. Gather environment/version/commit/procedure/test run evidence, skipped and failed tests explicitly.

### Required deliverables

Threat test execution report, CI/security test artifacts, retest evidence, residual risks, remediation owner list, independent QA/assurance summary.

### Verification and security-negative tests

NT-01 through NT-22 mandatory status report; keep each PASS/FAIL/NOT RUN/N/A with justification; add fuzz/property tests for IDs, status transitions, database isolation and input boundary.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Independent security reviewer and QA lead accept tests, false-positive review, retest results and residual blockers. CODEX must not self-approve or assume 100% security.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
