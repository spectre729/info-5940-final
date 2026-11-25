# Unit of work definitions

Status: Generated under the approved monolith decomposition plan; approved in chat; see audit.md. No Construction work is authorized. These documents define one application unit, five logical modules and a dependency-aware internal work sequence, not separately deployed services.

## U01: AI Job Application Agent

- Unit name for later artifacts: `job-application-agent`.
- Deployment: one local FastAPI/Uvicorn product process/worker, browser UI and shared secure local data boundary. Separate local security/collector facilities may be required by NFR/Infrastructure Design; they do not become extra product units or cloud services.
- Purpose: students/recent graduates confirm their background, discover recent relevant jobs, inspect evidence, save decisions, choose delivery and review existing bullet arrangements.
- Coverage: FR-01 through FR-10, NFR-01 through NFR-09, MVP-01 through MVP-06 and US-01 through US-18. All accepted security, resiliency and full PBT obligations apply.
- Primary unit accountability: whole team under the shared AI-DLC workflow. Responsibility areas below are mapped to README Parts 1-4; individual owners remain unassigned. This does not assign people or edit role claims.
- Exclusions: networking, recruiter search, essays, interview/OA monitoring, direct LinkedIn connection/scraping, invented resume claims, automatic applications/outreach, multi-user accounts and cloud hosting.

## Logical modules

### M01: Local foundation and safeguards

- Components: C02, C10, C11, C12.
- Responsibility area: Part 3 for runtime/data/recovery; Part 1 for process/record; cross-part security review.
- Individual owner: Unassigned until team claim.
- Scope: Access/session/key boundaries, encrypted persistence, protected audit/status and consistent backup/restore contracts. All services inherit policy ports; one app principal must not gain audit edit/delete rights.
- Required integration: approved typed methods in component-methods.md; shared IDs/version/evidence/error DTOs must remain compatible.

### M02: Profile and evidence interpretation

- Components: C03, C06.
- Responsibility area: Part 4 primary; Part 3 reviews shared gateway/storage contracts.
- Individual owner: Unassigned until team claim.
- Scope: Import and confirmation/version/provenance plus a reusable bounded model gateway/validator for extraction, tool intents, explanations and existing-bullet proposals.
- Required integration: approved typed methods in component-methods.md; shared IDs/version/evidence/error DTOs must remain compatible.

### M03: Discovery and shortlist

- Components: C04, C05, C07.
- Responsibility area: Part 3 primary for adapters/scans; Part 4 for fit/evidence evaluation.
- Individual owner: Unassigned until team claim.
- Scope: Supported APIs/pasted/fixture evidence, persisted asynchronous runs, lock/catch-up, freshness/dedup, fit and saved state; no LinkedIn automation.
- Required integration: approved typed methods in component-methods.md; shared IDs/version/evidence/error DTOs must remain compatible.

### M04: Reviewed bullet arrangement

- Components: C08.
- Responsibility area: Part 4 primary; Part 2 reviews approved product scope.
- Individual owner: Unassigned until team claim.
- Scope: Propose ordered unique existing confirmed IDs; original text rendering and explicit accept/reject without canonical-profile rewrite.
- Required integration: approved typed methods in component-methods.md; shared IDs/version/evidence/error DTOs must remain compatible.

### M05: Delivery and web composition

- Components: C09, C01.
- Responsibility area: Part 3 for delivery; Part 4 for review UI; Part 2 for journey acceptance.
- Individual owner: Unassigned until team claim.
- Scope: Separate delivery submodule C09 from final web composition C01; in-app default/opt-in SMTP and authenticated accessible views/routes. Both remain in one application unit.
- Required integration: approved typed methods in component-methods.md; shared IDs/version/evidence/error DTOs must remain compatible.

## Greenfield code organization strategy

Planned application code stays at the repository root, outside aidlc-docs/. No directories or code are created by this document.

| Planned path | Responsibility |
|---|---|
| src/app/main.py | Application assembly and entry point, consistent with the accepted app.main import after packaging. |
| src/app/contracts/ | Shared typed IDs, snapshots, errors and ports; no service imports or secrets. |
| src/app/foundation/ | M01 access/data/recovery/observability adapters and policy boundaries. |
| src/app/profile/ and src/app/model_gateway/ | M02 confirmed profile and reusable bounded model interface/validators. |
| src/app/discovery/ and src/app/shortlist/ | M03 source adapters, scan lifecycle and recommendations/status. |
| src/app/bullets/ | M04 reviewed existing-bullet arrangement. |
| src/app/delivery/ | M05-D C09 application delivery and SMTP adapter; does not import the web package. |
| src/app/web/, src/app/templates/, src/app/static/ | M05-W C01 route/views and local assets; imports/injects services, never the reverse. |
| tests/unit/, tests/property/, tests/integration/, tests/fixtures/ | Example, generated and integration checks with synthetic profiles/listings and provider doubles. |
| config/ | Non-secret example configuration and approved local runtime/deployment configuration. |
| pyproject.toml and uv.lock | Package src/app and lock selected verified dependencies during Construction. |
| data/ | Ignored private runtime artifacts; encryption and permissions required, ignoring alone is insufficient. |
| aidlc-docs/construction/job-application-agent/ | Future per-unit design and Markdown summaries only, never application source. |

The technical environment's startup command is an early sketch; the accepted security amendment requires a design-approved HTTPS/auth/encrypted runtime. Do not call the plain HTTP sketch compliant. Exact packages, versions, keys, collector isolation and startup commands require verified NFR/Infrastructure choices before implementation.

## Internal work packages and acceptance checkpoints

This sequence organizes work inside U01, not separately approved units or a bypass of per-unit design/code-generation gates.

1. Shared contracts and M01: establish ID/version/evidence/error interfaces, secure data/access/audit/recovery boundaries and synthetic repository tests before private-data flows. Preserve auth/audit failure handling.
2. M02: implement confirmed-profile workflow and shared bounded model port with deterministic doubles; profile versions and claim sources survive persistence/restart.
3. M05-D delivery boundary: establish in-app persisted views, opt-in/recipient contract and mock SMTP so the scan coordinator has a downstream contract without requiring web routes.
4. M03: integrate adapters, asynchronous scan lifecycle, normalization, freshness/dedup, evidence and status. Verify interrupted scans, active-run reuse, partial failures and no closed-app work.
5. M04: integrate selected-job proposal/acceptance using existing confirmed IDs and original text; reject/stale cases cannot mutate canonical claims.
6. M05-W final composition: assemble authenticated accessible web journey and result polling; test all features/security/consent/error paths together.
7. U01 integration/evaluation: example plus PBT, dependency scans, protected audit/access checks, local backup restore and reproducible fixture demo; test live configured providers separately without pretending fixture replay is live retrieval.

Part 1 coordinates workflow and evidence; Part 2 validates product/story consistency and presentation; Parts 3/4 own technical areas as described, with cross-part review. No task is assigned to an individual until claimed in the team process.

## Definition of done and remaining gates

Inception unit approval requires this definition, the dependency matrix and story map to cover all approved components/requirements/stories without cycles or hidden ownership gaps, plus per-rule extension ownership. It does not mean the product is implemented.

Future U01 Construction must execute Functional Design, NFR Requirements, NFR Design, local Infrastructure Design, approved Code Generation and Build and Test. Preserve explicit CI/rollback/deployment-style/incident/resilience-test decisions; select and configure PBT at its proper stages. Resolve auth/encryption/key custody/TLS/audit protection, backup cadence/retention/key recovery and deletion/restore semantics before using personal data. Demonstrate encrypted Backup and Restore with RTO 4 hours/RPO 24 hours and evidence-backed matching; no production SLA or additional cloud deployment is implied.

No individual module is complete until its integration and applicable security/recovery/generated/example-test obligations are satisfied. Shared C06 code is reused, not cloned. Unit approval is followed by a milestone documentation check and a stop before Construction.
