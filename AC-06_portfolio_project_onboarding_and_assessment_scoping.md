# AC-06 — Portfolio, Project Onboarding and Assessment Scoping

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Let tenant users register software systems and define clearly bounded assessments without pretending to know unseen assets.

**Prerequisites:** Accepted organizations, schema and versioned control registry.

You are implementing **only Phase AC-06** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Implement project/application/environment inventory with owner, business criticality, data classification, release version, architecture artifacts, repository references and risk profile.
2. Build project onboarding wizard and reusable risk questionnaire with transparent scoring logic (if used), manual validation and supporting evidence fields.
3. Select framework versions and applicability; enforce approval of exclusions/N/A with written reason and reviewer identity.
4. Create `assessment_scope` snapshot: exact assets/environments/source commit (if available), required controls, time window, authorized testing scope and reviewers.
5. Implement draft/review/approved/locked scoping states and permission-based edit restrictions; changes produce new immutable revisions.
6. Provide dashboard for gaps: no repository connected, missing architecture document, outdated version, unassigned reviewer and untested controls.

### Required deliverables

Portfolio UI, intake forms, data validation, risk context, scope review workflow, immutable assessment-scope snapshots, audit logging.

### Verification and security-negative tests

Bad tenant project ID; missing criticality; unauthorized scope edit; stale version, N/A approval missing; snapshot immutability; no generated/assumed architecture claims.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Product and assurance reviewers can independently reproduce scope and identify missing evidence; no unreviewed N/A exclusions counted as verified.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
