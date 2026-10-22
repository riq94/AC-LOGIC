# AC-14 — Continuous Monitoring and Production Operations

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Track changes that invalidate assurance and run AC Logic dependably without uncontrolled scans or data collection.

**Prerequisites:** Accepted release decisions, GitHub events, queues, reports and scoped operational ownership.

You are implementing **only Phase AC-14** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Subscribe to limited GitHub events and authorized schedules; detect new commit, dependency updates, changed control-relevant files, exception expiry and source deletion.
2. Mark old scan outcomes as commit-scoped/stale; trigger bounded re-evaluation jobs only under customer policy, quotas and accepted scopes. Never automatically perform active testing of unapproved targets.
3. Implement queue visibility, retry policies, backoff, dedup, dead letters, job cancellation, tenant resource quotas and error alerts.
4. Establish infrastructure monitoring, structured sanitized logs, tracing, SLO indicators, performance budgets, incident alerting, ownership and runbooks.
5. Design/test encrypted backups with periodic restoration in safe environment, retention and recovery expectations, rollback for app and database migrations.
6. Define data deletion, GitHub uninstall/policy revocation, key rotation and compromised integration response procedure.
7. Establish product status page/report mechanisms and corrective action operational workflow.

### Required deliverables

Monitoring dashboard and alert rules; bounded reassessment; per-tenant quota; restore and rollback drill records; incident/deletion/rotation runbooks.

### Verification and security-negative tests

NT-07, NT-12, NT-16, NT-18, NT-19, NT-22; webhook flood, job retry storm, worker timeout, stale scan marked, expired exception, restore test, deleted organization cleanup, downtime alert.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Platform owner reviews measured recovery exercise and operational alerts; security reviewer confirms no scope expansion/unauthorized scanning.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
