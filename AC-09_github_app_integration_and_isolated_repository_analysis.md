# AC-09 — GitHub App Integration and Isolated Repository Analysis

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Connect GitHub read-only and run tightly sandboxed analysis while preserving tenant isolation and reproducible scan evidence.

**Prerequisites:** Tenant controls, evidence vault, findings workflow and explicit authorization to install GitHub App for owned test repositories.

You are implementing **only Phase AC-09** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Register/configure approved GitHub App with minimal read permissions and human-visible consent/installation ownership flow; no PAT as default. Obtain installation ID and map it to exactly authorized tenant/projects and selected repositories.
2. Implement secure webhook endpoint validating raw-body HMAC-SHA256 using constant-time comparison, event-type allowlist, unique delivery id/dedup, replay protection and ignored unknown events; handle install/uninstall/permission changes.
3. Fetch fixed-commit snapshots read-only via short-lived installation tokens. Implement refresh/revoke and strict token handling; do not let tenant A choose tenant B installation ID or repo.
4. Add job queue with org/project/snapshot scope, idempotency keys, retries/cancellation, bounded quota, accurate status, sanitized audit.
5. Build ephemeral isolated worker with no app DB administrator key, restrictive filesystem, CPU/memory/time/disk limits, blocked metadata/internal addresses and tightly controlled network egress. Static text parsing first; never auto-run `npm install`, package scripts, CI workflows, repo binaries or Dockerfiles.
6. Integrate a small initial vetted analyzer set (secret detection, dependency/SBOM manifest review, static rule reports) with pinned tool version, rules and evidence format. Findings begin as `tool_detected`; do not auto-promote to verified.
7. Build connection, sync, scan status and finding-candidate UI; preserve source commit and stale-scan indication.

### Required deliverables

GitHub App install/permission flow, secure webhook and event inbox, read-only scoped fetch, sandbox worker, job orchestration, analyzer adapters, per-commit evidence metadata and uninstall behavior.

### Verification and security-negative tests

NT-01, NT-06–NT-10, NT-12, NT-18, NT-22; invalid HMAC/malformed signature; same delivery replay; cross-installation swap; expired token; installation revoked; malicious postinstall/CI file; egress/metadata denied; worker resource exhaustion.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Security lead witnesses webhook tamper tests, tenant installation isolation, worker sandbox boundary tests and validates no arbitrary untrusted execution. GitHub App permissions are reviewed and authorized.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
