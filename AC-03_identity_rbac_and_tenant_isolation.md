# AC-03 — Identity, RBAC and Tenant Isolation

## CODEX TASK PROMPT (paste after Master Directive and AGENTS.md)

**Objective:** Implement secure multi-tenant organization/project identity and prevent unauthorized cross-tenant access at every layer.

**Prerequisites:** Passing foundation CI; approved user/role matrix and Supabase environment controls.

You are implementing **only Phase AC-03** of AC Logic. Before changes, read `AGENTS.md`, `00_MASTER_DIRECTIVE.md`, applicable `reference/` policies, accepted ADRs, prior phase evidence and repository reality. Conduct a **read-only preflight** and deliver a proposed file/API/database/testing plan with security implications. Do not invent existing implementations. Obtain human approval for substantial writes and all sensitive actions. Do not deploy, access production secrets or test external targets without separate explicit authorization.

### Implementation tasks

1. Configure Supabase Auth or approved identity equivalent; implement invite flow, session lifecycle, MFA requirement for high-privilege roles, member revocation and account recovery protections.
2. Implement org and membership tables with unique keys, role grant/revocation audit, authorization policy service, request context derived from verified identity and zero-trust organization switching.
3. Establish RLS on every tenant-owned exposed table, review SQL GRANT privileges and test SELECT/INSERT/UPDATE/DELETE, RPC and views. Enforce tenant ownership in server API and storage keys.
4. Enforce role separation: org_owner/org_admin/engineering_lead/developer/security_reviewer/assurance_approver/auditor_readonly/platform_operator. Prevent developer self-approval and privileged role escalation.
5. Add invitation-expiry and revocation, account lock/rate controls, MFA guard for privileged approval paths and scoped service-role usage as documented exception only.
6. Build Organization management UI with clear access-denied and activity history. No admin-without-login capability.

### Required deliverables

Identity/role APIs and UI; migrations; RLS policies; tested roles matrix; service credential callsite inventory; identity/tenant threat update.

### Verification and security-negative tests

NT-01–NT-06, NT-17, NT-19; anon/owner/developer/reviewer/removed-user CRUD; view/RPC bypass; profile tampering; org ID rewrite; storage read; MFA/role change audit; concurrent role revocation.

Run actual lint, type, unit, integration and affected database checks; report each as PASS/FAIL/NOT RUN with output references. For requirements needing manual testing, specify exact procedure and reviewer. Never use mock results to claim security or assurance completion.

### Human acceptance gate

Security reviewer independently verifies all defined cross-tenant denial cases, reviewed policies and absence of service-role token in client bundles. Any tenant bypass blocks phase acceptance.

### Mandatory handoff output

Provide: (1) implemented vs deferred scope; (2) exact changed paths and migrations; (3) relevant permission/tenant trust boundaries; (4) actual checks and results with evidence; (5) known risk and rollback plan; (6) reviewer approvals required; (7) recommendation to accept or block—**not** a self-issued acceptance. Stop at this gate.
