# AC-17 — Optional IoT and OT Assurance Extension (Post-MVP)

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Extend AC Logic for authorized IoT/OT devices and systems without treating ordinary SaaS as industrial automation or risking live equipment.

**Prerequisites:** Explicit new product approval after validated general SaaS product; additional OT/security subject matter experts and isolated lab.

You are implementing **only Phase AC-17** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Define separate device/gateway/cloud/firmware asset model, trust boundaries, device inventory, safety classifications and operating constraints.
2. Build optional framework registry and licensing for NIST SP 800-213, ETSI EN 303 645 and ISA/IEC 62443 where applicable; source and scope verified.
3. Review device identity, firmware signing/update integrity, secure provisioning, telemetry/MQTT authorization, key rotation, revocation and edge-to-cloud trust boundaries.
4. Add evidence imports for static firmware manifests, SBOM, gateway config, network zone diagrams and passive lab traces. Never scan production ICS or safety-critical devices by default.
5. Create device-specific review templates, specialist reviewer rules, controlled lab approvals, separate risk decision authority and safety impact checklist.
6. Pilot strictly in isolated owned testbeds with stop rules and no live operations access.

### Required deliverables

Optional module ADR, IoT asset/requirements models, device assurance templates, lab-only verification and safe pilot report.

### Verification and security-negative tests

Wrong device/tenant access; unauthorized firmware writes; unsigned update indicated (not performed); data leak; inappropriate live scanner attempts denied; lab test safety checklist.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

OT/IoT specialist + security + product approval, licensed standards handling and lab safety review. Not required for general SaaS launch.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
