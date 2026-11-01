# RSKNEX — KILO MASTER IMPLEMENTATION DIRECTIVE
Version 1.0 | 2026-11-01 | Owner: Rsknex product team
Repository: GnMohareb/Rsknex
Working branch: assessment/canadian-cu-foundation
Status: EXECUTION SPECIFICATION — NOT A CLAIM THAT FEATURES EXIST

## 0. Mission and authority
Build an Ontario-credit-union-focused Governance, Risk & Compliance MVP using the existing SimpleRisk-based repository as a potential foundation. The MVP must be a cohesive operational product, not a collection of forms or mockups. Kilo is the implementation agent; this file defines required work, sequencing, proof and stop conditions. Do not silently substitute a new framework, delete existing functionality, invent regulatory obligations, or claim readiness without tests.

Work autonomously through each stage, making small reviewable commits and maintaining status files. Ask for input ONLY for genuine blockers: legal licensing, unavailable secrets/credentials, unresolvable upstream restrictions, irreversible infrastructure changes, or major architecture tradeoffs not settled here. Do not wait for approval after ordinary engineering subtasks.

## 1. Hard boundaries
- Do NOT modify production deployments or customer data. Use local/test fixtures and synthetic data only.
- Do NOT commit secrets, passwords, tokens, private keys, real member records or proprietary SimpleRisk Extras.
- Preserve attribution and all applicable upstream license notices; verify license for every reused component before commercial claims.
- Do NOT assume GPL/AGPL/MIT/MPL obligations without reviewing actual files and dependencies. Record findings and flag counsel review.
- Do NOT make claims of FSRA certification, approval or regulatory compliance.
- Keep source-to-obligation mapping reviewed and versioned. Do not invent law text or binding status.
- Prefer isolated application + database + storage per institution for MVP. No shared cross-institution database by default.
- No broad refactoring until baseline app runs and characterization tests protect existing behavior.
- No AI-based compliance decisions in MVP; any future AI is advisory and human-approved.
- Never call an untested or stubbed feature complete.

## 2. Stage gates and execution order
### G0 — Baseline evidence (weeks 1–2)
1. Clone and inventory complete repository (file tree, language/runtime, build files, installer, database migrations/schema, auth, roles, API, scheduled jobs, storage, tests, workflows, third-party libraries, license notices).
2. Record exact source commit, release tag, runtime versions and hashes. Note README states public SimpleRisk code is a release mirror with private upstream.
3. Create docs/audit/REPO_INVENTORY.md with evidence paths and verified/unverified flags.
4. Create docs/audit/LICENSE_AND_DEPENDENCIES.md with component, version, license evidence, attribution obligations, security status, SaaS implications, and unknowns.
5. Stand up reproducible LOCAL development using existing supported tooling. If containerization is suitable, add compose and Dockerfiles without deleting native installation support. Seed ONLY synthetic demo data.
6. Capture baseline screenshots and map all existing functions to requirements in docs/audit/FEATURE_GAP_MATRIX.md: EXISTING/EXTEND/NEW/BLOCKED with exact code paths and test evidence.
7. Add CI lint, unit smoke tests and dependency/security scans compatible with discovered stack.
**Exit:** documented clean install works, login and basic risk workflow verified, license inventory sufficiently reviewed for development, no critical untriaged vulnerabilities.

### G1 — Security and institution boundary (weeks 3–5)
1. Create institution-aware deployment configuration, provisioner and environment validation; one app/database/storage boundary per institution.
2. Define RBAC roles: Platform Operator (provisioning only), Institution Admin, Risk Manager, Compliance Officer, Control Owner, Internal Auditor, Executive/Board Viewer, Read-only Reviewer.
3. Deny-by-default access policies, segregation of duties, per-record authorization, audit trail for create/update/delete/approval/download/login; UTC timestamps and actor identifiers.
4. MFA/SSO capability decision based on actual stack; require MFA for privileged access; no homemade cryptography.
5. Encrypted transport, secrets from environment/secret manager, safe file upload with MIME/size controls and malware-scanning integration point, evidence download authorization.
6. Threat model STRIDE-style, cross-institution negative tests, backup/restore rehearsal, logging redaction.
**Exit:** automated privilege escalation and cross-institution negative tests pass; documented restore works.

### G2 — Unified data model and core workflows (weeks 5–9)
Canonical entities and links (reuse existing schema when safe):
Institution, User, Role, BusinessUnit, Process, Risk, RiskAssessment, RiskAppetite, TreatmentPlan, KRI, Control, ControlTest, Evidence, Finding, CorrectiveAction, Approval, Comment, ActivityEvent, RegulatorySource, Obligation, ObligationVersion, ApplicabilityAssessment, ControlMapping, Vendor, VendorAssessment, ReportSnapshot.
Every relevant record includes stable ID, institution scope, owner, status, timestamps, lifecycle and provenance. All schema changes reversible and migration-tested.
Risk journey: create -> classify -> inherent likelihood/impact -> treatment -> linked controls -> residual likelihood/impact -> approval -> review date -> KRI -> report.
Compliance journey: source -> obligation/version -> applicability decision -> control map -> evidence -> assessment -> exception -> corrective action -> verification -> report.
Control journey: assign -> describe frequency -> collect evidence -> test -> conclude effective/ineffective -> open finding.
Finding journey: create -> owner and due date -> action plan -> evidence -> independent validation -> close or reopen.
Vendor journey: register -> criticality -> due diligence -> approval -> reassessment schedule. Keep this lean.
Approval state transitions must be enforced server-side; reject invalid states and self-approval where segregation is required.
**Exit:** integration tests demonstrate linked records and complete workflows with zero manual database intervention.

### G3 — Ontario regulatory content (weeks 7–11)
Source register must cover, subject to applicability and qualified review:
- Ontario Credit Unions and Caisses Populaires Act, 2020 and applicable regulations.
- FSRA Sound Business and Financial Practices Rule.
- FSRA Risk-Based Supervisory Framework (supervisory assessment methodology; not automatically a binding obligation).
- FSRA Operational Risk and Resilience guidance.
- FINTRAC AML/ATF requirements as applicable.
- Applicable privacy, governance and consumer protection requirements.
Each item: regulator, jurisdiction, authoritative URL, document identifier, source type [LAW/RULE/GUIDANCE/SUPERVISORY/OPTIONAL], published/effective/review dates, version, exact clause reference, short analyst summary, applicability, reviewer, approval date, mapping rationale, change log.
No unverified scraped text should be represented as authoritative. Do not copy large copyrighted source passages. Link to source and store concise, reviewed summaries.
Implement source version comparison, changed-obligation review queue, applicability decisions, and traceable control mapping.
**Exit:** at least one representative approved sample for each source category, complete source-to-control-to-evidence-to-report trace, human review status visible.

### G4 — UX, reporting and operational quality (weeks 10–13)
Create role-based coherent IA:
Dashboard / My Work / Risks / Compliance / Controls / Evidence / Findings & Actions / Vendors / Reports / Administration.
Navigation must preserve context, breadcrumbs, ownership, statuses, due dates, search, filter, bulk operations only when safe, empty states, validation messages, responsive layouts and accessible labels.
Core dashboards: open risks by severity, overdue actions, control effectiveness, obligations by status, audit findings, upcoming reviews. Never fabricate KPI values.
Board pack: as-of timestamp, approved risk heatmap, top risks, regulatory exceptions, overdue remediation, control effectiveness, management commentary, evidence lineage, CSV/PDF export where feasible.
**Exit:** task-based UAT by each role; keyboard/accessibility baseline; board numbers reconcile with source records.

### G5 — Harden and release candidate (weeks 13–16)
- Unit, integration, E2E and negative authorization suites in CI.
- Dependency vulnerability triage and remediation; no unresolved critical/high findings without written risk acceptance.
- Performance tests with realistic synthetic institution data, evidence storage and report generation.
- Penetration test by qualified independent reviewer (external dependency; mark BLOCKED until performed).
- Restore drill, incident runbook, support runbook, change management, rollback and release notes.
- Pilot onboarding package, privacy/data handling, data retention/export/deletion policies reviewed by qualified advisers.
**Exit:** all P0 acceptance tests pass, independent security gate cleared, pilot readiness signed off. Otherwise status remains NOT READY.

## 3. Acceptance tests (must automate where possible)
AT-01 Fresh developer setup from README succeeds with no undocumented manual steps.
AT-02 Risk owner can create, assess and treat a risk; residual risk calculation is deterministic and auditable.
AT-03 Compliance officer can create versioned source, record applicability, link control and evidence, and generate traceability report.
AT-04 Control owner can upload evidence; unauthorized user cannot access it even by direct URL or ID.
AT-05 Reviewer can reject or approve; submitter cannot self-approve where policy prohibits.
AT-06 Findings cannot close without required evidence and independent verification.
AT-07 Vendor reassessment due date appears in My Work and dashboard.
AT-08 Board viewer sees only approved/reportable information and cannot mutate records.
AT-09 Institution A cannot view, search, export or download Institution B data; automated negative tests.
AT-10 Audit events capture actor, object, action, time and change provenance without leaking secrets.
AT-11 Reports reconcile to underlying filtered records and display as-of time.
AT-12 Source status explicitly distinguishes draft, reviewed, approved, superseded and withdrawn.
AT-13 Backup restored into isolated environment and data integrity verified.
AT-14 No synthetic fixtures or demo credentials exposed in production build.

## 4. Required documentation and artifacts
Maintain:
- docs/audit/REPO_INVENTORY.md
- docs/audit/LICENSE_AND_DEPENDENCIES.md
- docs/audit/FEATURE_GAP_MATRIX.md
- docs/architecture/ADR-001-FOUNDATION.md
- docs/architecture/ADR-002-TENANT_ISOLATION.md
- docs/architecture/DATA_MODEL.md
- docs/architecture/SECURITY_THREAT_MODEL.md
- docs/regulatory/SOURCE_REGISTER.md
- docs/product/USER_JOURNEYS.md
- docs/product/SCREEN_INVENTORY.md
- docs/testing/ACCEPTANCE_MATRIX.md
- docs/operations/LOCAL_SETUP.md
- docs/operations/DEPLOYMENT_AND_ROLLBACK.md
- docs/operations/BACKUP_AND_RESTORE.md
- docs/status/IMPLEMENTATION_STATUS.md
- docs/status/BLOCKERS.md
Do not create empty placeholder docs; each must contain evidence, decisions, links to implementation, or clearly marked TODO with owner.

## 5. Delivery protocol
1. Start by reading this directive and the prior foundation assessment.
2. Perform G0 before adding product features. Inspect first; do not guess file paths or dependencies.
3. Work in feature branches from a known baseline; never force-push or overwrite user work.
4. For each unit of work: identify requirements IDs, inspect relevant code, implement, add tests, run tests, document results, commit with descriptive message.
5. Keep IMPLEMENTATION_STATUS.md with columns: requirement, status [NOT_STARTED/IN_PROGRESS/BLOCKED/TESTED/ACCEPTED], commit, test command, evidence, blocker.
6. Never count code existence as functional completion; require running test or validated walkthrough.
7. Update BLOCKERS.md immediately when blocked. Continue independent tasks where safe.
8. Create pull requests for review with summary, migration impact, test evidence, security impact, screenshots for UI and rollback.
9. Do not merge into master until review gates are satisfied.
10. At each stage, report DONE, PARTIAL and BLOCKED with explicit evidence; no optimistic percentage scores without measurable acceptance criteria.

## 6. Immediate Kilo instruction
Execute G0 now. First inventory the actual source tree and license/dependency evidence, then establish a reproducible local build and run baseline smoke tests. Create the named audit artifacts, populate the feature-gap matrix with verified evidence, and propose ADR-001/002. Do not start new Canadian modules before the baseline and licensing gates are resolved. Continue autonomously through nonblocked work and report concrete commits, tests and remaining blockers.

## 7. Reference
Related assessment: docs/assessment/CANADIAN_CREDIT_UNION_GRC_FOUNDATION.md.
Official source domains for verification: fsrao.ca, ontario.ca/laws, fintrac-canafe.canada.ca, priv.gc.ca. Use authoritative current documents and cite URLs and effective dates in the source register.
