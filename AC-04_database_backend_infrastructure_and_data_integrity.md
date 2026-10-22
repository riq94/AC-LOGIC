# AC-04 — Database, Backend Infrastructure and Data Integrity

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Deliver domain schema and secure transactional application service layer with integrity guarantees.

**Prerequisites:** AC-03 organization policies accepted.

You are implementing **only Phase AC-04** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Create consistent schema for projects, environments, components, repositories metadata, standards, assessments, evidence, findings, remediations, jobs, approvals and audit events; phase in tables needed by later modules.
2. Use composite tenant-aware keys/foreign keys, meaningful unique/check constraints and strict enumerated workflow transitions. Enforce RLS and grants on each migration.
3. Implement typed repository/domain interfaces and API validation with uniform authorization middleware/policies; never let frontend dictate ownership.
4. Define transaction boundaries for state changes, optimistic concurrency or locks for approval workflow, and idempotency keys for queued/event operations.
5. Implement schema migration process using disposable database/staging first, documented up/down or forward recovery and backup/restore expectations.
6. Maintain API contracts and seed only synthetic demo data; avoid hidden assumptions about live Supabase schema.

### Required deliverables

Versioned PostgreSQL migrations, typed API/domain layer, constraints and RLS; schema diagram, data dictionary, migration/rollback runbook.

### Verification and security-negative tests

Composite FK invalid cross-org reference, duplicate membership, invalid state/value, concurrent writes, rollback and full fresh-DB migration; NT-04, NT-06, NT-17, NT-20.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

DB and security lead accept migration diffs, constraints, privileged paths and all relevant migration/RLS test logs before extending schema.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
