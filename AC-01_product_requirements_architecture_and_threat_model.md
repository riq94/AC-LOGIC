# AC-01 — Product Requirements, Architecture and Threat Model

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Convert product vision into implementable functional/non-functional contracts and a reviewable threat model before scaffolding.

**Prerequisites:** Accepted AC-00 inventory and explicit architecture-planning authority.

You are implementing **only Phase AC-01** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Prepare detailed PRD, personas, roles matrix, user journeys for Build-with-AC-Logic and Review-with-AC-Logic, MVP exclusions and accessibility targets.
2. Propose modular monolith domains, HTTP API contracts, async jobs and security boundary diagrams; document frontend/backend/deployment stack tradeoffs.
3. Model data assets and trust boundaries: end-user, auth provider, API, PostgreSQL/RLS, object storage, GitHub connector, worker, LLM gateway and operational logs.
4. Threat-model STRIDE-style cases: cross-tenant IDOR, reviewer self-approval, worker breakout, webhook spoofing, prompt injection, evidence tampering, exfiltration and supply-chain compromise.
5. Create ADRs for Supabase/Auth architecture, GitHub App vs tokens, AI consent policies, evidence integrity, private storage and customer deletion.
6. Define versioned standards ingestion/licensing, policy enforcement, quality gates, performance and recovery objectives proposed for approval.

### Required deliverables

docs/PRD.md; docs/architecture/{context,containers,trust-boundaries}.md; docs/adr/*.md; docs/threats/threat-model.md; docs/roles-and-permissions.md; docs/MVP-scope.md.

### Verification and security-negative tests

Peer-review threat model against every entry in reference/SECURITY_CONTROL_BASELINE.md; verify every MVP feature has testable acceptance criteria, API owner and explicit non-goal.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Human architecture + security leads sign off ADRs, product scope, key boundaries and risk decisions. No cloud creation or coding without later authorization.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
