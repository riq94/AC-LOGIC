# AC-02 — Repository Foundation, CI and Design System

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Create reliable development foundation and functioning secure app shell without prematurely implementing domain workflows.

**Prerequisites:** Approved AC-01 ADRs, toolchain and human approval to create/change local repository files.

You are implementing **only Phase AC-02** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Scaffold approved Next.js/TypeScript strict monorepo or follow accepted repo layout. Use package manager and lockfile, reproducible installs, formatting, linting, typechecking and test runners.
2. Establish private repo conventions: branch protection recommendations, CODEOWNERS, pull-request template, commit discipline, versioned AGENTS.md, issue templates and security disclosure policy.
3. Implement accessible UI shell with navigation, responsive page layout, error/empty/loading states, tokens, reusable tables/forms and keyboard access.
4. Establish CI with lint, typechecks, unit/integration placeholder suites, dependency scanning, secret scanning, migration validation when DB exists and restricted workflow permissions; prefer pinned trusted actions.
5. Add safe `.env.example`, local onboarding, logging conventions, runtime config validation, health/readiness endpoints and local dev/test docs.
6. Establish architecture records and a build-evidence report template; no service-role secrets in client bundles.

### Required deliverables

Working app shell; lint/type/test configuration; CI workflow; repo templates; documented local setup; first CI run evidence and required branch protection settings.

### Verification and security-negative tests

Fresh clone/install/build succeeds; lint/type/unit baseline runs; intentionally invalid env fails safely; accessibility smoke checks; CI permissions examined; secret scan reports no committed credentials.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

CI and local reproducibility accepted. Do not claim branch protection enabled until verified in GitHub settings.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
