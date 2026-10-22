# Reference — Stage gates and production go/no-go rules

## Every phase: G0–G7

| Gate | Required approval evidence | Owner |
|---|---|---|
| G0 — Scope | Codebase inspection, approved bounded task, explicit non-goals, risk level | Product + engineering lead |
| G1 — Design | API/data contracts, affected tenants, threat implications, approved ADR when needed | Architecture lead |
| G2 — Implementation | Changes satisfy acceptance criteria; critical scope items not replaced with mock behavior | Engineering lead |
| G3 — Automated verification | Actual lint/type/unit/integration/migration results; CI results match commit | Engineering + QA |
| G4 — Security | Updated threat controls, negative tenant/role tests, scan findings, independent review where required | Security lead |
| G5 — Evidence | Evidence chain/accuracy, no fabricated scan or standards outcomes; report tied to commit/source | Assurance reviewer |
| G6 — Operational | Rollback, monitoring, alerts and incidents considered; new secrets/config documented | Platform lead |
| G7 — Human acceptance | Owner signs off approved scope and authorizes next phase; outstanding risks recorded | Designated approver |

A blocked gate cannot be re-labeled as a warning to continue. An authorized, documented scope change can move requirements to later phases, but cannot remove security invariants or invent a pass.

## MVP entry (after AC-08 + basic AC-13)

- Organization membership, RBAC and tenant-scoped data/storage tests pass on staging.
- Standards/versions imported with provenance and legal/license review; ASVS L2 mapping visibly scoped.
- Full manual assessment and finding/remediation/retest workflow exists; reviewer self-approval denied.
- Evidence stored privately, hashed, retrieved by authorized reviewers and audited.
- At least one end-to-end report displays verified vs unverified coverage; report cannot claim compliance certification.
- Threat model has no outstanding release-blocking findings for the MVP functions.
- Basic CI, tests, backup/restore practice and logging in place.

## Beta entry (after AC-09–AC-13)

- GitHub App validated end to end: minimal permission, installation mapping, HMAC, event dedup, uninstall, token rotation/expiry.
- Isolated workers cannot reach cloud metadata, other tenants or app control-plane secrets; resource limits measured.
- Tool-generated findings remain candidates unless verification evidence exists; AI cannot forge results or grants.
- Reviewer separation and release gate negative tests succeed; exports tied to exact snapshots.
- At least two seeded reference apps assessed and false positives/false negatives recorded.

## Production go/no-go (AC-16)

**Block** release if any of the following is true:
1. Confirmed cross-tenant access, critical authorization flaw, secret disclosure, worker breakout or broken approval independence.
2. Unresolved policy-blocking critical finding without a specifically permitted, documented, independently approved exception; certain issues (e.g. cross-tenant breach) cannot be excepted under default policy.
3. Required ASVS Level 2 control is presented as passed without adequate procedure/evidence or when scope exclusions lack approval.
4. Data integrity, audit signing/evidence provenance or historical standards-version integrity tests fail.
5. Required staging disaster restore and rollback are untested/failed.
6. Required MFA/auth/access lifecycle control failures.
7. Missing legal review on standards redistribution/AI data processing where relevant.
8. Insufficient monitoring, incident owner or release ownership.

Require explicit release record containing: commit SHA/build digest, database migration set, scan/test results, known issues, residual risk register, business owner, independent assurance signoff, platform owner, go/no-go timestamp and rollback procedure.

## Risk acceptance policy

Acceptances require issue/control ID, confirmed current test outcome, impact/likelihood, tenant(s)/environment/asset scope, business owner, independent reviewer, compensating controls, expiry, reassessment condition and revocation method. Expired acceptance automatically becomes invalid; `verified_fail` stays visible. Disallow ordinary admin override of segregation of duties.

## Completion declaration

Each phase report must end with one of: `ACCEPTED`, `REJECTED`, `PARTIALLY ACCEPTED WITH EXPLICIT SCOPE CHANGE`, or `BLOCKED`. CODEX cannot issue a final acceptance on the human approver's behalf: it may recommend a state and request recorded confirmation.
