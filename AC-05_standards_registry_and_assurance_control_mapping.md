# AC-05 — Standards Registry and Assurance Control Mapping

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Create a versioned provenance-backed standards registry without inventing normative controls or unauthorized reproduction.

**Prerequisites:** AC-04 secure schema, legal/standards review for control import rights.

You are implementing **only Phase AC-05** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Implement framework/version/requirement/crosswalk/import provenance data and UI. Support NIST SSDF 1.1 final, ASVS 5.0.0 stable; ISO 27001:2022 Amd1 2024 and SOC 2 criteria as licensed/authorized metadata/readiness maps.
2. Source ASVS IDs from a verified official 5.0.0 artifact; preserve versioned `v5.0.0-X.Y.Z` identifiers, level attributes and attribution/license fields. Validate parsing and checksum before import.
3. Distinguish final publications from drafts; SSDF v1.2 draft must not replace the 1.1 baseline. Retain source URLs, import timestamps, verifier and original license metadata.
4. Implement control applicability proposal and human approval, review profile targeting ASVS L2 based on SaaS sensitivity, and exclusions with rationale.
5. Build human-reviewed crosswalks with partial/related relationships instead of false one-to-one equivalence.
6. Make published versions immutable and maintain historical report references after subsequent imports.

### Required deliverables

Versioned import CLI/service, checksum and license documentation, standards browser/control detail, crosswalk workflow and approved Level 2 scope template.

### Verification and security-negative tests

Wrong-version ID rejected; duplicate control import idempotent; draft segregated; later import does not rewrite prior assessment; permission for edit/publish enforced; NT-15.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Security/assurance lead verifies sampled control IDs against official source and licenses before marking imported controls usable. No AI-generated control text accepted as official.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
