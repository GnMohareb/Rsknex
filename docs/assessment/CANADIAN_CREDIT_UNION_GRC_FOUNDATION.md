# Rsknex — Canadian Credit Union GRC Foundation Assessment

Status: IN PROGRESS — not production approved
Date: 2026-11-01
Branch: assessment/canadian-cu-foundation

## Product objective
Commercial GRC SaaS for Canadian credit unions, starting with provincially regulated Ontario institutions. Reuse SimpleRisk core only where licensing, security, and upgradeability are verified. Maintain institution-specific isolation and regulator-specific content.

## Verified repository observations
- The fork's README describes SimpleRisk as a release mirror; upstream development is private and releases arrive as snapshots.
- The GitHub repository is accessible and a dedicated assessment branch has been created.
- License-file, dependency, and full architecture verification are NOT complete. Do not infer a legal conclusion from repository visibility.

## Non-negotiable gates
1. Legal: inventory every source license, bundled dependency, commercial Extra and trademark condition. Obtain legal review of proposed modifications, SaaS hosting and distribution.
2. Security: review auth/session/authorization, vulnerabilities, secrets, dependencies, logging, evidence access, backup/restore and encryption. Perform independent penetration testing before pilots with real data.
3. SaaS: demonstrate strict tenant separation; prefer isolated deployments and databases initially. Test cross-tenant access, admin boundaries, export and deletion.
4. Regulatory: distinguish binding obligations from supervisory guidance and voluntary standards. Record authoritative URL, regulator, jurisdiction, document version, effective date, applicability, mapping rationale and human reviewer.
5. Operational: establish CI/CD, tests, release tracking, patch process, incident response, recovery objectives and change control.
6. Usability: validate end-to-end user journeys with risk, compliance, audit and board personas.

## Regulatory content packs
### Ontario initial pack
- Credit Unions and Caisses Populaires Act, 2020 and regulations
- FSRA Sound Business and Financial Practices Rule
- FSRA Risk-Based Supervisory Framework (supervisory assessment, not standalone binding obligations)
- FSRA Operational Risk and Resilience guidance
- Applicable AML/ATF (FINTRAC), privacy, consumer protection and governance requirements

### Future packs
- Federal credit unions: OSFI and federal legal requirements
- Other provinces: regulator-specific requirements and applicability rules
- Optional standards: ISO 27001, NIST CSF, SOC 2 as licensed/appropriately referenced mappings

No regulatory compliance claim is approved until qualified Canadian counsel or subject-matter experts verify applicability and current wording.

## Unified conceptual data model
Institution -> business unit -> process -> risk -> assessment -> treatment -> control -> test -> evidence -> finding -> remediation.
RegulatorySource -> Obligation -> Applicability -> ControlMapping -> Assessment -> Evidence.
Vendor -> Criticality -> DueDiligence -> Contract -> Monitoring -> Incident.
All records require owner, timestamps, change history, permissions and institution boundary.

## MVP workflows and acceptance tests
1. Risk: identify, assess inherent/residual risk, approve treatment, monitor KRI and report. Test permission checks and calculation auditability.
2. Compliance: import versioned obligation, approve applicability, map controls, collect evidence, assess and remediate. Test source traceability.
3. Vendor: register, classify criticality, approve due diligence and schedule reassessment. Test segregated approval.
4. Audit: plan, test, issue finding, remediate and independently verify closure. Test immutable event history.
5. Resilience: inventory critical operation, run BIA, record test and corrective action.
6. Board: generate dated pack with exceptions, trend data and drill-through lineage.

## Prioritized backlog
P0: verify repository structure, licenses, dependencies and installation; establish reproducible isolated dev environment.
P0: document baseline features and map to MVP journeys with screenshots/tests.
P0: threat model and tenant isolation architecture; prevent member-level data ingestion in initial pilots.
P0: regulatory source register and human validation process.
P1: unified navigation, risk/control/obligation/evidence relationships, role workflows and reporting.
P1: CI/CD, vulnerability scanning, backup/restore and monitoring.
P2: AI-assisted control mapping with citations, approval and strict no-training data controls.
P2: integrations and subscription provisioning.

## Go/no-go decision
Do not proceed to production or ingest confidential institutional data until all P0 gates pass. Do not assume SimpleRisk proprietary Extras are available in the fork. Any core modifications must be tracked separately from proprietary extensions and reviewed for license compliance.

## Immediate next evidence needed
- Full file tree and relevant license notices
- Dependency manifests and lockfiles
- Application bootstrap/install procedure
- Authentication/authorization and data model inventory
- Functional workflow walkthroughs in running instance
- Threat model, remediation estimates and costed architecture
