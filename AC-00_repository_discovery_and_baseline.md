# AC-00 — Repository Discovery and Baseline

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Inspect the actual repository, inventory assets and configurations, identify risks and propose work without inventing pre-existing integrations.

**Prerequisites:** Private repository and human-approved read-only inspection scope.

You are implementing **only Phase AC-00** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Inspect repository tree, dependency manifests/lockfiles, framework/tool versions, Git status and branches; record current commit and existing CI tests.
2. Inventory deployments/environments, domains, credentials *by name only*, database schemas, Supabase environments, code ownership and third-party processors without outputting any secret.
3. Build a route-to-database/dataflow inventory, initial tenant trust-boundary diagram, risks and gap analysis against approved decisions.
4. Write a prioritized requirements register with IDs, owners, status and supporting proof. Classify product features as MVP, beta or later.
5. Identify missing information as BLOCKER/ASSUMPTION rather than guessing. Identify safe local/staging prerequisites and candidate ADRs.

### Required deliverables

docs/discovery/inventory.md; docs/discovery/data-flows.md; docs/discovery/gaps-and-risks.md; docs/requirements/backlog.md; docs/adr/ADR-000-proposal.md. No application code or production changes.

### Verification and security-negative tests

Read-only checks: repo status/commit, dependency listing, known tests where harmless. Verify all listed deployments have an evidence source; no secrets leak in outputs. Confirm no application write in discovery.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Human product/engineering/security review approves the inventory, prioritized MVP boundary, authorization of subsequent phase and unresolved blockers. Stop without implementation.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
