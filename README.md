# AC Logic — CODEX Master Development Prompt Pack

**Prepared for:** Access Cube  
**Date:** 22 October 2026  
**Purpose:** A structured, phase-gated implementation package to build AC Logic using CODEX.

## Approved foundation
General SaaS first · Multi-tenant SaaS · PostgreSQL/Supabase · GitHub first · ASVS 5.0.0 Level 2 default target · Human-controlled AI authority.

## Contents
- `00_MASTER_DIRECTIVE.md` — paste into CODEX once to establish the authoritative mission and guardrails.
- `AGENTS.md` — place at the Git repository root; adapt paths only after discovery.
- `phases/` — execute `AC-00` through `AC-17` *one at a time*, gated by human review.
- `reference/ARCHITECTURE_AND_DATA.md` — suggested architecture, domain boundaries, SQL/RLS and evidence entity design.
- `reference/SECURITY_CONTROL_BASELINE.md` — actionable security baseline.
- `reference/TEST_AND_THREAT_MATRIX.md` — positive, negative, malicious input, data integrity and reliability tests.
- `reference/ACCEPTANCE_GATES.md` — completion, go/no-go and human sign-off criteria.
- `reference/REUSABLE_CODEX_PROMPTS.md` — prompts to inspect, implement, review, remediate and hand off.
- `reference/STANDARDS_AND_LICENSES.md` — verified primary references and licensing caveats.
- `reference/CONTROL_MAPPING_TEMPLATE.csv` — starter schema, not an invented official control import.

## Safe execution order
1. Create a **new private** GitHub repository with protected default branch and restricted permissions. Do not commit secrets or customer data.
2. Put `AGENTS.md`, this pack and appropriate documentation in the repo.
3. Paste the master directive into CODEX and allow **read-only discovery**.
4. Execute `AC-00`, review outputs and manually approve the next task.
5. Use `AC-01` architecture and threat review, `AC-02` CI/quality, then core MVP phases `AC-03` through `AC-08`.
6. Add GitHub integration and analysis workers only after tenant isolation, evidence integrity and policy authorization have passed.
7. Complete remaining phases and pilot validation. Optional IoT/OT phase `AC-17` is **explicitly out of MVP**.
8. Independently verify each phase with `reference/REUSABLE_CODEX_PROMPTS.md`. Do not auto-merge or auto-deploy.

## Priority sequence
**MVP:** AC-00–AC-08 and initial AC-13 reporting.  
**Engineering automation:** AC-09–AC-11.  
**Independent assurance / production:** AC-12–AC-16.  
**Optional extension:** AC-17.

## What this pack does NOT do
This is a **development prompt specification**, not a completed application, a tested repository, certification, legal advice, cloud deployment or penetration-test authorization. Run all implementation steps against the actual repository. Standards statuses may change; re-verify authoritative sources at implementation time.
