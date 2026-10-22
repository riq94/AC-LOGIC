# AC-07 — Private Evidence Vault, Provenance and Audit

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Store sensitive technical evidence privately, traceably and with tamper detection.

**Prerequisites:** Accepted tenant/RLS isolation and project scope workflows.

You are implementing **only Phase AC-07** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Configure private object storage and approved upload flow with org/project authorization, MIME/type and extension checking, file-size limits, safe names, content hashing, malware/quarantine strategy and data classification.
2. Persist artifact source, uploader, environment/commit, tool version, collection time, retention, SHA-256, reference integrity and explicit consent for AI processing.
3. Use expiring authorized download URLs or proxied stream authorization, revocation semantics, protected exports, evidence versioning and retention/deletion workflow.
4. Implement append-only audit events for access, upload, download, approve, delete, permission changes and hashes; consider independently secured immutable event exports.
5. Link evidence to individual verification procedure/control/finding; mismatch, missing source or stale commit must invalidate reliance on evidence.
6. Add scoped evidence upload/list/detail viewer with audit history and restricted download. Prevent source excerpts in ordinary operational logs.

### Required deliverables

Evidence API/UI, private storage policies, artifact hash verification, custody/audit records, retention runbook, secure signed URL handling.

### Verification and security-negative tests

NT-01, NT-05, NT-11, NT-12, NT-16; wrong tenant object, forged path, changed bytes/hash, oversized and disguised upload, expired link, unauthorized delete, log redaction.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Security reviewer performs cross-org storage attack tests and confirms integrity indicators are enforced, not cosmetic. Deletion policy approved.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
