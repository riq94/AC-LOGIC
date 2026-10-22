# AC-13 — Executive Dashboard and Assurance Reporting

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Create accurate transparent reports with evidence navigation and clear limitations; no fabricated security scores.

**Prerequisites:** Sound source data in project, assessment, evidence and finding domains; for MVP implement basic report earlier if AC-09+ deferred.

You are implementing **only Phase AC-13** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Build tenant/project portfolio dashboard with filters, review coverage and missing evidence, unresolved risk, stale assessments, remediation aging, blocked releases and actionable reviewer queues.
2. Report independently: scoped applicable controls, verified pass/fail, not tested, insufficient evidence, N/A approved, accepted risk, coverage of required controls, evidence freshness and decision status.
3. Create technical finding detail and executive summary formats with severity rationale, business impact, source evidence, owner, date, controls and remediation status.
4. Export PDF/CSV/JSON using sanitized scoped queries and immutable snapshot references; ensure 'AI-assisted analysis' vs independently verified finding labels are visible.
5. Disclose standard version, scope, assessment date, excluded assets, methods, pending tests, limitations and reviewer approvals. Never claim ISO/SOC2 certification/attestation.
6. Add report integrity metadata (hash, generation version, who generated, evidence/source snapshot) and signed/access-controlled download strategy where required.
7. Handle large datasets with server pagination/aggregation and permission-aware caches. No leak through charts or counts.

### Required deliverables

Executive/technical dashboard, detailed report pages, correct CSV/JSON/PDF exports, scoped filters, metadata and audit for generation/download.

### Verification and security-negative tests

NT-01, NT-05, NT-12, NT-14, NT-15; wrong tenant reports, empty assessment, 100 passes+1 critical fail, risk accepted vs pass, version drift, PDF text escaping, XSS from finding titles, large export bounds.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Independent reviewer samples report numbers against raw audit/evidence/control records and confirms truthful limitations, privacy and release label semantics.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
