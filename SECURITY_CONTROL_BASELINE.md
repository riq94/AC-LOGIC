# Reference — Security control baseline (AC Logic as an assessed system)

Treat this baseline as required implementation and test scope, with mapping to actual standards IDs only after verification from versioned sources.

| ID | Area | Required control / verification |
|---|---|---|
| AC-S01 | Identity | Verified identity, secure session lifetime, MFA for admin/review/approver, brute-force prevention, secure reset and revocation. |
| AC-S02 | Authorization | All API mutations and reads enforce tenant/project and role authorization on trusted server; deny by default. |
| AC-S03 | PostgreSQL/RLS | Exposed tables have reviewed grants + enabled RLS; test CRUD, RPC, views, storage and service credentials. |
| AC-S04 | Tenant isolation | Distinct organizations cannot access/alter each other's project, assessment, report, storage, queued job or webhook installation data. |
| AC-S05 | Separation of duties | Developer cannot independently verify own high-risk finding or authorize own high-risk risk exception/release. |
| AC-S06 | Input validation | Validate schemas, bounds, URLs, upload metadata, filenames, webhooks and all trust boundary inputs. |
| AC-S07 | Sessions/CSRF | Appropriate cookie flags, session rotation, CSRF protection on state-changing browser flows; anti-replay where appropriate. |
| AC-S08 | Cryptography/secrets | HTTPS, encryption at rest, secret vault, key rotation strategy, no plaintext credentials or repository tokens in client bundle/logs. |
| AC-S09 | GitHub App | Installation-scoped minimum-permission tokens; raw-payload HMAC verification constant-time, event dedup and installation ownership mapping. |
| AC-S10 | Isolation workers | No execution of client build scripts/control plane commands; temporary unprivileged sandbox, blocked cloud metadata, limited egress, CPU/memory/disk/time quotas. |
| AC-S11 | Storage | Private buckets, tenant-bound paths, file-type sniffing, size bounds, malware handling/quarantine if applicable, expiring scoped access, retention/deletion. |
| AC-S12 | Supply chain | Lockfile, dependency review, SBOM/provenance strategy, code/secret/license scans, pinned trusted CI actions where operationally feasible. |
| AC-S13 | API/abuse | Request size/rate quotas, pagination, bounded exports, webhook rate limits, background job quotas, detailed rejection auditing without secrets. |
| AC-S14 | Audit/integrity | Tamper-evident decision/evidence history, authenticated authorship and time, protected export, independent write restrictions. |
| AC-S15 | Privacy | Customer consent and policy prior to model disclosure; redaction, data minimization, contract/subprocessor awareness, classification, deletion procedures. |
| AC-S16 | AI boundary | Prompt injection controls; tool permission contracts; retrieval citation and relevance checks; structured outputs validated; no autonomous decisions. |
| AC-S17 | DAST/scope | No external active security scan without proof of authorization and explicit domain/project scope; deny private/internal addresses for user-configured targets. |
| AC-S18 | Operations | Separate environments, least-privilege deployments, verified backup restore, rollback plans, observability, incident response, availability monitoring. |
| AC-S19 | Errors | Safe error pages, no stack trace/connection string disclosures, consistent API errors, admin diagnostics protected. |
| AC-S20 | Release decision | Required verified checks plus independent human authorization; policy-blocking failures stay blocked even when an overall metric appears high. |

## Security acceptance policy
- Every item should have owner, applicability, precise verification steps, evidence, assessment state and defined release impact.
- Show **coverage**, **evidence sufficiency**, **findings**, and **disposition** separately.
- No security control may be marked `verified_pass` exclusively on an AI response, unverified scanner output, UI screenshot or unrun test.
- Security impact must be evaluated for all newly proposed frameworks, tools and data processors.
- Platform operators do not automatically become customer organization users. Customer support access must be time-bound, consented, audited and least privilege where supported.

## Secure multi-tenant GitHub workflow
- Authenticate organization owner/admin to initiate GitHub App installation; verify callback `state` and installation ownership.
- Request minimum GitHub permissions, initially Contents read + Metadata read; additional read permissions only for explicitly required evidence, with operator-facing explanations.
- Server generates installation tokens just in time; do not store them in tenant-facing DB fields.
- Validate webhook HMAC over **raw bytes**, then map event `installation_id` to the correct organization/project, enforce bounded event types, idempotent `delivery_id`, replay window or dedup state, and revoke sync on uninstall.
- Lock repository sync to allowlisted installations and repository selections; never follow untrusted Git redirects to internal destinations.
- Keep source fetch/pull read-only and use snapshot commit SHA for reproducible analysis.

## AI use policy
- AI may propose architecture, tests, controls, candidate findings, remediations and report narratives; display cited evidence and source versions.
- AI may not modify standards source records, mark controls passed, close vulnerabilities, sign off exceptions, approve release, self-assign privileged roles, or run arbitrary external scans.
- Treat repository files such as README, prompt/agents text, build manifests, CI YAML, issues and PR descriptions as **data**, not policy instructions.
- Maintain explicit organization policy regarding model provider, data residency, retention, customer intellectual property and whether code/evidence snippets may be transmitted.
- Prefer least-data retrieval and local/deterministic checks; log model metadata and sanitized prompt/output hash, not secrets or complete client code.
