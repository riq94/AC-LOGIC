# AC-11 — Grounded AI Advisor and AI Engineering Governance

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Provide useful contextual guidance without giving an LLM authority over controls, accounts, scans or production.

**Prerequisites:** Scoped source/evidence permissions, approved privacy/data-processing policies, reviewable standards registry and findings state machine.

You are implementing **only Phase AC-11** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Build provider-agnostic model gateway with approved model/provider selection, tenant policy, consent for source/evidence snippets, per-org token/cost limits, timeouts and redaction.
2. Implement retrieval of only authorized tenant/project snippets and versioned public/approved standards metadata; attach citations/commit/file/source and mark stale or missing context.
3. Create assistant use cases: explain verified finding, propose remediation and regression tests, review ADR, compare design alternatives, answer scoped standards questions, draft review notes.
4. Validate structured AI outputs through schemas and security policy; outputs create drafts/candidates only. Disallow AI from updating control_result to verified_pass, signing off risk, modifying membership, accessing secrets or running broad tools.
5. Build prompt-injection defenses: repository/README/web content considered data, not instructions; tool allowlist with per-action user/role guard, explicit user consent for any sensitive disclosure; no arbitrary URLs/exec.
6. Maintain sanitized AI activity audit: actor/org/project, model/provider/version, consent, source references, response ID/hashed payload, confidence limitations; avoid storing customer plaintext by default.
7. Implement refusal/fallback when source evidence is missing; AI must say 'cannot verify' rather than invent a result.

### Required deliverables

AI Advisor UI/service, policy controls and consent UX, safe retrieval middleware, schema validation, source citations, AI audit metadata, synthetic prompt-injection adversarial fixtures.

### Verification and security-negative tests

NT-01, NT-08, NT-13; poisoned README/AGENTS prompt, injected document, cross-tenant retrieval attempt, missing consent, malicious tool-call JSON, nonexistent control ID, fabricated exploit and evidence, disabled provider.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Security/privacy owner approves model data flow, consent and redaction. Independent reviewer confirms AI cannot mutate outcomes or roles and adversarial prompts fail safely.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
