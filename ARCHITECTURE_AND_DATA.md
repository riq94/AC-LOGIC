# Reference — System architecture, domain contracts and data model

This document is a **proposed reference**, not permission for CODEX to implement before Phase AC-01 acceptance. All decisions should become accepted ADRs.

## Logical architecture

```
Browser / Tenant Users
      |
 CDN + WAF + HTTPS + auth/session controls
      |
 Next.js web / server API (trusted identity + policy enforcement)
      |
 +-------------------------+-------------------------+
 | Domain services         | Connector gateway        |
 | - organization/project  | - GitHub App installation|
 | - scopes/assessment     | - webhook HMAC verifier  |
 | - standards registry    | - minimal scoped tokens  |
 | - findings/risk         | - idempotent events      |
 | - evidence/approval     |                          |
 +------------+------------+------------+------------+
              |                         |
       Postgres/Supabase            Trusted job queue
      (RLS + constraints)                 |
              |                 Ephemeral isolated workers
     Private object storage       static analysis/metadata
     (tenant-scoped keys,         no arbitrary scripts/eval
      content digest)                    |
              +-------------AI advisory gateway---------+
                            redaction, consent,
                         grounding, structured outputs
```

Separate development, staging and production projects/accounts; treat CI/admin tools as privileged.

## Suggested domain packages

`apps/web`, `apps/worker`, `packages/domain`, `packages/db`, `packages/policy`, `packages/standards`, `packages/evidence`, `packages/integrations/github`, `packages/analysis`, `packages/ai`, `packages/ui`, `tests/security`, `docs/adr`, `docs/threats`, `docs/assurance`.

Do not adopt this folder layout blindly if the inspected repository already has a safe architecture.

## Domain entity inventory and constraints

| Domain | Entities | Key invariants |
|---|---|---|
| Identity | organizations, profiles, memberships, roles, invitations, sessions metadata | authenticated membership; uniqueness of `(org_id,user_id)`; MFA for privileged actions |
| Portfolio | projects, applications, environments, repository_connections, source_snapshots, releases, components, ADRs | unique ownership, foreign keys, repository installation mapped to exactly authorized org/project |
| Standards | frameworks, framework_versions, requirement_versions, crosswalks, review_profiles | immutable published versions; stable versioned requirement key; source/license provenance |
| Assurance | assessment_templates, assessments, scoped_requirements, procedures, control_results, verification_runs | result references exact standards revision, project scope and snapshot; status transitions authorized |
| Evidence | artifacts, evidence_links, artifact_versions, fingerprints, tool_attestations | immutable digest/size/source metadata; restricted private object path; deletion/retention auditable |
| Findings | candidate_findings, confirmed_findings, severity, remediation_tasks, retests, false_positive_reviews | no automated promotion to verified exploit; findings do not disappear when remediated |
| Decision | reviewer_assignments, risk_acceptances, approver_attestations, release_gate_runs, overrides | no self-approval; reason/owner/expiry for risk acceptance; gate decision signed and auditable |
| Async | jobs, job_attempts, event_inbox, outbox_events, integration_credentials references | idempotency keys, retry caps, dead letter path, tenant-scoped jobs |
| AI | advisor_sessions, requests, model_outputs, citations, consent_grants | AI cannot write control results or approvals; redact and honor consent flags |
| Ops | audit_events, retention_policies, alerts, notification_outbox | append-only audit history / external immutable log; sensitive event integrity |

### Common fields
Most tenant-owned records should contain `id`, `organization_id`, `project_id` when applicable, `created_at`, `updated_at`, `created_by`, `schema_version` or business version as needed. Sensitive records additionally include `recorded_by`, `source_ref`, `source_version`, `content_sha256`, and `retention_until` where relevant.

### Relational protections
- Foreign keys must prevent cross-tenant references: favor `(organization_id, id)` composite uniqueness and same-organization composite FKs for tenant-owned relationships. Do not rely exclusively on `organization_id` columns being equal by convention.
- Check constraints for statuses, valid severity/risk domains, expiry > issue date and bounded numeric values; explicit unique constraints; transactions and row locking for multi-step updates.
- Audit trails should preserve **before/after** for controlled business transitions without unnecessarily logging personal or secret data.
- Use separate `verification_result` and `risk_disposition`: failing verification can have `risk_accepted` disposition but remains failed.
- Never silently mutate previously issued assessment report snapshots or overwrite an earlier standards version.

## RLS and Supabase principles
1. Enable RLS on exposed tenant tables and explicitly reduce schema grants; **RLS alone does not retract broad SQL GRANT permissions**.
2. Restrict rows to membership in the corresponding organization; implement reusable security-definer helpers sparingly, with safe search_path and review to avoid privilege escalation.
3. Tenant identity must derive from authenticated subject and server-validated org membership; not from untrusted request body or client-stored role claims.
4. Verify `SELECT`, `INSERT`, `UPDATE`, `DELETE`, upsert, `RETURNING`, bulk endpoints, nested joins, views, RPCs, realtime subscriptions and storage operations.
5. Reject attempted tenant ID rewrites and same-ID collisions; test deletion of membership and revoked sessions.
6. A Supabase server secret/service-role credential bypasses RLS in certain contexts; restrict it to service functions with explicit validated org scope and document every callsite.
7. Run DB tests with several organization/user identities and also unauthenticated, disabled and stale members.

## Finding and evidence contract

Suggested `Finding` fields: id, organization_id, project_id, assessment_id, source (`human`, `rule`, `AI`), classification (`hypothesis`, `tool_detected`, `human_confirmed`, `reproduced`, `false_positive`, `resolved_verified`), CWE/CVE if verified and applicable, severity with rationale, likelihood/impact, affected asset, source code location and commit, evidence list, remediation owner/due date, detection time, verification procedure, reviewer, approval history.

Suggested `EvidenceArtifact` fields: id, tenant/project, MIME/type and size, storage key (not public URL), SHA-256, uploading principal, collection timestamp, source URI/ref, source commit, tool/verifier versions, environment, classification/sensitivity, expiry/retention, consent for AI use, evidence validation result, reference counts, audit events.

Evidence custody: require cryptographic hash validation on ingest, restricted reads, immutability or version preservation as designed, signed ephemeral download when authorized, append-only audit stream in separately protected storage. Hash alone does not prove evidence authenticity; trusted collection and independent validation also matter.

## Release gate policy

Default `BLOCK` when: missing required control verification, tenant isolation failure, unresolved policy-blocking critical issue, report/evidence integrity failure, no required independent signoff, or unverified recovery/rollback capability for release policy. `REVIEW_REQUIRED` for insufficient evidence where allowed; `READY` only after required policy checks and human approver decision. An approved exception is always explicit, scoped, expiring and separate from control verification fact.
