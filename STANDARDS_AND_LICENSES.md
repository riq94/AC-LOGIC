# Standards registry — source, status, intellectual property and version management

**Reference check date: 2026-10-22. Recheck before production imports.** This file points to authoritative content but does not reproduce copyrighted standards in full.

| Source | Version/status for baseline | Source URL | Integration restrictions |
|---|---|---|---|
| NIST SP 800-218 SSDF | 1.1 final | https://csrc.nist.gov/pubs/sp/800/218/final | Version key + task identifiers; use official text under applicable publication terms. |
| NIST SP 800-218 Rev.1 | 1.2 initial public draft, NOT final | https://csrc.nist.gov/pubs/sp/800/218/r1/ipd | Track proposed differences separately; never treat draft as approved requirement. |
| OWASP ASVS | 5.0.0 stable | https://asvs.owasp.org/downloads/ | Use versioned `v5.0.0-X.Y.Z` IDs; comply with CC BY-SA 4.0 attribution/share-alike requirements for redistributed material/adaptations. |
| ISO/IEC 27001 | 2022, with Amd 1:2024 | https://www.iso.org/standard/88435.html | ISO text has controlled licensing; store independently authored summaries and legally acquired/approved references only. Do not embed wholesale text without rights. |
| SOC 2 Trust Services Criteria | 2017 criteria (revised points of focus 2022) | https://www.aicpa.com/resources/download/2017-trust-services-criteria-with-revised-points-of-focus-2022 | AICPA rights apply; readiness control mapping is not an audit or attestation. |
| NIST AI RMF / GenAI Profile | AI RMF and AI 600-1 | https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence | Advisory for model risk, data handling and trustworthy AI. |

## Standards import design requirements

- `framework`, `framework_version`, `status`, `published_at`, `source_uri`, `checksum`, `license_id`, `attribution_text`, `ingest_rights_review`, `imported_by`, `verified_by`.
- `requirement_version` has versioned identifier, parent section, applicability levels, controlled title/reference, testing guidance metadata and source commit/URL.
- `mapping` has relationship type (`related`, `supports`, `partial_overlap`), confidence, independent reviewer, evidence and rationale. A mapping is **not** a claim that frameworks have identical requirements.
- `applicability_decision` records scope, inclusion/exclusion, person approving, date and reason. N/A without a rationale should be rejected.
- Keep all published versions immutable; new versions add crosswalks rather than overwriting older requirement contents or previous assessment outcomes.
- Differentiate **technical verification of an application's controls** (ASVS) from **organizational governance and assurance readiness** (ISO 27001/SOC 2). Do not calculate an overall compliance percentage by simply adding unrelated standards controls.

## Labels the product may display

Prefer: `ASVS 5.0.0 L2 assessment coverage`, `NIST SSDF practice review`, `ISO 27001 readiness mapping`, `SOC 2 control evidence readiness`.

Avoid: `ISO-certified`, `SOC 2 attested`, `NIST-approved` or `OWASP-certified` unless a separate legitimate authority/contract explicitly supports the precise claim.
