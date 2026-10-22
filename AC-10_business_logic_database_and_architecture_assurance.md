# AC-10 — Business Logic, Database and Architecture Assurance

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Turn architectural/business/database reasoning into concrete review procedures and verifiable tests, not speculative pass labels.

**Prerequisites:** Accepted manual assurance engine and safe analysis foundations; sample SaaS requirements and isolated synthetic database fixtures.

You are implementing **only Phase AC-10** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Create architecture inventory workflow: components, integrations, boundaries, ADRs, service ownership, capacity/availability assumptions, change-impact references and traceable review findings.
2. Add backend/API review procedures for authentication/authorization, parameter validation, error handling, timeouts, idempotency and API schemas; retrieve only scoped source.
3. Add PostgreSQL/Supabase assessment rules and human review procedures for grants/RLS/views/SQL functions, referential constraints, migrations, indexes, locks and backups. Do not connect to production database with elevated credentials unless separately authorized.
4. Implement business-rule specification and evidence linking for approvals, value/precision boundaries, transaction atomicity, fraud-relevant workflows, concurrency, refunds/voids, multi-tenant invariants and valid state transitions.
5. Support import of existing tests and query plans as evidence, plus safe suggested tests and fixture generation in authorized sandbox.
6. Distinguish static heuristic from verified runtime behavior; display tool confidence and false positive dispute workflow.

### Required deliverables

Architecture review templates/UI; database/backend control procedures; testable business invariants; deterministic rule adapters; findings with reproducible sources and reviewer decisions.

### Verification and security-negative tests

Seeded test apps with broken RLS, inconsistent FK, race-prone double-posting, invalid rounding, missing server validation, unsafe migration and transaction rollback; reject fabricated test runs.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Engineering reviewer proves significant findings against owned fixtures, can challenge false positives, and confirms no production DB or customer code execution beyond scope.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
