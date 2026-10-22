# AC-16 — Pilot Validation and Commercial Production Hardening

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Validate AC Logic against real authorized customer workflows and prepare responsibly for commercial launch.

**Prerequisites:** Phase AC-15 verification, operational readiness and explicit agreements with pilot owners.

You are implementing **only Phase AC-16** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Choose three consented pilot types: AI-built SaaS in development, an existing operated SaaS, and a seeded vulnerable sample. Document repository ownership, data processing scope and authorization.
2. Execute full project registration→scope→assessment→evidence→findings→remediation→independent re-test→release recommendation→report lifecycle.
3. Collect outcomes: true/false positives, coverage vs applicable controls, average investigation time, evidence freshness, reviewer effort, usability and tenant privacy observations.
4. Validate enterprise customer controls: SSO roadmap, audit export, retention, security questionnaire, support access, incidents, subprocessors, SLAs and disaster recovery.
5. Conduct threat-model reassessment, independent code/security review and legal licensing/privacy review.
6. Execute non-production backup restore and rollback; create release manifest with commit/build digest, test results, migrations, incidents contact, known defects, release notes.
7. Present board/technical go-no-go pack with BLOCK/REVIEW_REQUIRED/RECOMMEND_READY and accountable human signatures. No direct live production deployment by CODEX.

### Required deliverables

Pilot reports and signed scopes, evaluation metrics, defect/remediation register, verified runbooks, audit/license review, commercial release candidate handoff.

### Verification and security-negative tests

Evidence that all reference/ACCEPTANCE_GATES.md production requirements are evaluated, known blockers cleared, end-to-end workflow run by independent humans, scoped data deletion and restore validated.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Separate engineering, security/assurance, product and platform leadership give formal written go/no-go. CODEX only prepares the evidence and recommendation.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
