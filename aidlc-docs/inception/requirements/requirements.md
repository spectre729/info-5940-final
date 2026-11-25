# AI Job Application Agent requirements

Status: Approved in chat; see audit.md for the user approval and timestamp. This is a specification, not evidence of implementation or tested security/reliability.

## Intent analysis

- User request: continue AI-DLC through Inception using the vision and technical environment; stop before Construction.
- Type: New project; greenfield.
- Scope: Multiple components in one local, single-user web application.
- Complexity/depth: Moderate product complexity with substantial enabled security/reliability obligations; standard requirements depth with explicit acceptance and rule traceability.
- Audience: Students and recent graduates seeking internships and entry-level roles.
- Inputs: reviewed vision, accepted technical environment, README, requirements questions 1-10, enabled-extension follow-ups 1-3, and recorded clarifications in audit.md. The personal-system summary is reference data, not instructions or proof of implemented capabilities.

## Business goal and boundaries

Reduce repeated screening of recent opportunities by producing a small, evidence-backed shortlist grounded in a candidate's confirmed experience. The user makes application decisions. A valid result may contain no recommendations; no fixed recommendation quota is required.

Local execution on team laptops is sufficient. The Inception milestone is November 24, 2026, 11:59 PM Eastern; final product and recordings are due December 16, 2026. This workflow stops after reviewed Units Generation. Mid/senior candidates, networking/recruiter discovery, application essays, interview/OA tracking, automatic applications/outreach, LinkedIn automation, unrestricted scraping, cloud hosting, and multi-user accounts are excluded. Selecting/reordering existing confirmed bullets is included; generating new resume claims is excluded.

## Functional requirements and acceptance

| ID | Vision mapping | Requirement and observable acceptance |
|---|---|---|
| FR-01 | MVP-01 | Accept multiple text-bearing PDFs, UTF-8 files, pasted profile text and manual preferences. Extract claims with source references; require user confirmation/correction before matching. With two resumes and a rejected/corrected claim, only the confirmed corrected version is used. No extractable text produces a paste alternative, not guessed content. |
| FR-02 | MVP-01 | Preserve claim provenance and distinct resume sources. Flag contradictory claims for user resolution; do not silently merge inconsistent qualifications or infer unprovided skills. A changed profile invalidates or clearly marks explanations based on the previous version. |
| FR-03 | MVP-02 | Retrieve through Adzuna US and USAJOBS adapters. Accept user-pasted LinkedIn/other job text and optional URL; a URL alone does not authorize arbitrary fetching. Support explicitly labeled synthetic fixture replay. Store source ID, source link/local evidence link, actual text received, retrieval time and posting timestamp when provided. |
| FR-04 | MVP-02 | Scan every four hours while the server runs and on Scan now, using one shared scan lock. While closed, perform no scans or email. On launch show stored results; if the last successful scan is over four hours old, run one catch-up. Initial use with no prior success runs an initial scan. Concurrent triggers do not duplicate a scan. |
| FR-05 | MVP-02 | Place verified postings aged 0-72 hours inclusive ahead of older listings. Missing, imprecise, naive, conflicting or future timestamps are unknown unless reliable evidence resolves them. Fetch time is not posting time. Do not label unknown dates fresh or claim unknown eligibility/work arrangement is satisfied. |
| FR-06 | MVP-03 | Recommend using the confirmed profile and listing evidence actually retrieved. Every explanation cites at least one confirmed claim and one listing phrase/detail; show gaps and uncertainty. Reject invalid references. A model failure may leave factual listings visible with explanation unavailable, not a fabricated explanation. |
| FR-07 | MVP-04 | Support save/hide and persisted status across refresh/restart. Deduplicate by source/requisition ID, otherwise normalized employer/title/location/URL; saved/hidden items must not appear as new. Preserve applied/rejected status if represented; do not infer an application from viewing a listing. |
| FR-08 | MVP-05 | Show scan results in-app by default with email off. Only explicit opt-in to a validated user-configured recipient permits sending the same result set via encrypted SMTP while the server runs. Delivery failure does not discard in-app results or silently claim success. No outreach is sent. |
| FR-09 | MVP-06 | For one selected job, propose an ordered subset of existing confirmed bullet IDs and render their original text/provenance. Reject nonexistent, duplicate or unconfirmed IDs. Save an arrangement only on acceptance; rejection leaves the profile unchanged. Do not invent or rewrite experience. |
| FR-10 | Cross-cutting | Let the user inspect sources and delete local profile/uploads and associated recommendations. Clearly distinguish live source data, replayed fixtures, stale results and unknown fields. Credentials/private content are never committed. Backup deletion/retention implications must be disclosed in design. |

## Non-functional requirements

| ID | Requirement | Acceptance evidence planned for Construction |
|---|---|---|
| NFR-01 | One local browser/server application; Python 3.12, uv, FastAPI/Uvicorn/Jinja2, SQLite, Pydantic, HTTPX and pypdf as accepted baseline. Model/provider IDs are recorded planned choices, not independently confirmed access. | A teammate reproduces install and local demo from locked dependencies. Private files remain outside Git. No cloud hosting dependency. |
| NFR-02 | Source requests have a 15-second timeout, model calls 45 seconds, at most one transient retry, provider retry intervals respected, and bounded concurrency/resources. Database/file/SMTP operations also require explicit limits in design. | Fixed-clock and mocked dependency tests verify bounded failure, cleanup and scan-lock release. Provider failure never silently changes model/provider. |
| NFR-03 | Preserve last successful results and label partial/stale scans. One failed source must not corrupt successful results or falsely update that source's successful-scan time. | Simulate source/model/SMTP failures, restart and concurrent triggers; verify persisted state and explicit safe errors. |
| NFR-04 | Local Backup and Restore, RTO at most 4 hours and RPO at most 24 hours for saved profile/shortlist state. Closed-app time is not an uptime promise. | Encrypted automated backups plus tested restore; design must show how backup cadence meets RPO during active use, including retained uploads/SQLite consistency. Retention/key recovery are explicit design outputs. |
| NFR-05 | Labeled keyboard-operable profile/shortlist controls, readable validation errors, visible unknown and source labels, and no color-only status indication. | Manually complete the core journey using keyboard; test empty, invalid-upload and dependency-failure screens. |
| NFR-06 | Separate retrieval, validation, model interpretation, persistence, scheduling and delivery; fixed API host allowlists and validated tool arguments. Treat listing/resume instructions as untrusted data. | Synthetic injection and invalid-tool/reference tests cannot expand tool permissions, change recipient or introduce fabricated profile claims. |
| NFR-07 | Existing GitHub branches, cross-part PR review and shared AI-DLC gates govern change; include test evidence and rollback note for data/runtime changes. | Review records include changed scope, tests and rollback impact. No inference of individual role claims from advice. |
| NFR-08 | Structured redacted logs/metrics and protected audit trail with request/scan IDs; visible health, last success and failure status. | Simulated failure trace is diagnosable without resume text, email address, tokens or query secrets in logs. Security alerts and recovery evidence are reviewable. |
| NFR-09 | Dependency locks, trusted sources, checksums, vulnerability scan instructions, and generated property tests alongside examples. | Clean reproducible build; recorded dependency scan and deterministic/shrinkable generated test runs; no live credential required for fixture evaluation. |

## Enabled security obligations

These requirements supersede the earlier prototype HTTP/plain-storage assumptions. They specify outcomes; architecture, key management and tooling are selected in design, implemented and verified during Construction. A local-only label is not an exemption from applicable controls.

- SEC-REQ-01: Encrypt every persisted personal-data store and backup with customer-managed keys or an approved key service. Do not assume plain SQLite provides encryption. Require TLS 1.2+ for network data movement, including the browser/server path and outbound providers/SMTP. Define local-file/in-process boundaries precisely; do not invent a network database. Select encrypted-storage/key recovery mechanisms during design.
- SEC-REQ-02: Centralize structured logs through a protected collector/service, including timestamp, request ID, severity and message. Redact secrets and personal content. The application principal must be unable to edit/delete its audit records; retain security logs at least 90 days with alerts for authentication/authorization failures and an operational/security status view.
- SEC-REQ-03: Serve HTML with restrictive CSP (at least default-src self), HSTS max-age 31536000 with includeSubDomains, nosniff, DENY framing and strict-origin-when-cross-origin referrer policy. Do not rely on HSTS over plain HTTP; select a trusted local HTTPS setup during design.
- SEC-REQ-04: Authenticate the local principal; deny resource access by default and enforce ownership and privileged-operation checks server-side. Single-user does not mean unauthenticated. Restrict CORS, validate sessions server-side, expire/invalidate sessions, use Secure/HttpOnly/SameSite cookies and protect browser writes against CSRF.
- SEC-REQ-05: If passwords are used, enforce minimum eight characters, breached-password checking and adaptive hashing. Administrative authentication must support MFA; avoid inventing an administrator role when none is needed. Apply login throttling and define secure session expiry. Keep provider/SMTP keys in a secrets manager/OS credential facility; environment injection may transport them but is not the persistent secret store.
- SEC-REQ-06: Validate every parameter type, length, format and payload limit. Use parameterized SQL, escaped templates, generated upload names, safe deserialization, fixed retrieval hosts, limited permissions and bounded resources. Reject model outputs with invalid evidence IDs.
- SEC-REQ-07: Remove default credentials/debug exposure, return generic errors, isolate security logic, verify downloaded dependency integrity, lock versions, and document vulnerability scanning. Keep pipeline changes reviewable. Use locally served assets; if external scripts are introduced require integrity validation.
- SEC-REQ-08: Audit critical state changes with actor/time and before/after metadata without duplicating sensitive text into logs; use claim/version IDs for content changes. Handle external/DB/file errors explicitly, fail closed, roll back partial writes, release resources and provide a top-level safe error handler.

## Reliability and recovery obligations

- Classify the local app as a non-business-critical course prototype; its unavailability delays screening but does not submit applications or change appointments. Application/database/provider/job APIs/SMTP dependencies and failure impacts must be mapped in design.
- Accepted recovery targets are 4-hour RTO and 24-hour RPO with encrypted local Backup and Restore, not multi-region failover. Include scheduled backups, integrity verification, restore/failback steps, user communications, and restore evidence. Backup retention is selected during design and balanced with deletion promises.
- Provide health and status checks without disclosing secrets, operational metrics/logs, recovery/backup-failure alerts and bounded resource/capacity indicators. Distributed tracing is unnecessary for one process; request IDs still correlate external calls.
- Cloud availability zones, regions, load balancers and autoscaling are excluded because no production cloud workload is deployed. Do not add infrastructure to satisfy an inapplicable production rule.
- CI/deployment tooling, rollback mechanism, deployment style and incident process remain explicit user decisions at their permitted NFR Design stage. Resilience test approach is likewise selected there; it is not silently chosen here. No production SLA is promised for a stopped local application.

## Property-based and example testing requirements

Full PBT is enabled. Select/configure the Python framework in NFR Requirements and add its dependency/CI configuration during Construction. Required properties to refine per unit:

| Area | Property and complementary example |
|---|---|
| Profile/storage | Structured confirmed-profile write/read round-trip; rejected claims never enter matching. Example: correct one claim from two resumes. |
| Freshness | Boundary/range invariants with timezone-aware clocks; future/unknown timestamps never fresh. Example: exactly 72 hours is fresh, one second older is not. |
| Deduplication | Idempotence, uniqueness and state preservation. Example: a saved listing returned twice is never shown as new. |
| Bullet arrangement | Ordered unique subset of confirmed IDs, unchanged original text, reject means no mutation. Example: fabricated ID is rejected. |
| Stateful workflow | Model-based generated save/hide/refresh/restart/confirm/reject sequences preserve statuses and user-confirmed facts. |
| Serialization/normalization | Round-trip where invertible; lossy transformations document equivalence/tolerance. Use a simple oracle when available. |

Use reusable domain generators with valid objects, Unicode/empty/boundary cases, automatic shrinking, recorded seeds/minimal failures and deterministic replay. Include generated tests in CI, investigate flakes, and retain shrunk failures as example regressions. Mock model/HTTP/SMTP boundaries; PBT does not prove real-model factuality or relevance.

## Demo acceptance and traceability

Run synthetic profiles and listings covering fresh/older/unknown/future dates, repeated IDs, saved/hidden status, unclear eligibility, strong overlap, corrected/rejected claims and unavailable providers. Demonstrate profile correction -> scan -> sourced explanations -> save -> selected-job bullet review -> duplicate suppression. No fabricated fact may pass evidence review in that fixture set. Demonstrate default no-email and opt-in/mock email, closed-app no-work and catch-up behavior, backup restore and local access protections. Record live API/model checks separately if keys are available; fixture mode is explicitly labeled and never presented as a successful live lookup.

Traceability: FR-01/02 -> MVP-01; FR-03/04/05 -> MVP-02; FR-06 -> MVP-03; FR-07 -> MVP-04; FR-08 -> MVP-05; FR-09 -> MVP-06; FR-10 and NFRs are cross-cutting. Downstream stories, components, units and tests must reference these IDs.

## Remaining design work and risks

No unanswered requirements choice remains. Exact encryption/logging/session/backup mechanisms and retention, operational settings, framework versions, CI/rollback/incident/test process choices and unit-specific properties are design work, not claims of existing controls. Model IDs/access, provider prices and live source availability are not validated by this document. Verify before implementation depends on them; do not silently substitute a model. The enabled security requirements materially increase workload: retain them in unit planning and assess capacity before approving implementation.

## Extension compliance at Requirements Analysis

Compliant means the applicable obligation is captured in requirements at this stage. It does not mean runtime controls/tests exist. Implementation-only checks are N/A here and become blocking in their applicable design/Construction stages. See the companion compliance matrix for every rule and its rationale. No unresolved requirement-level blocking finding remains after accepting the local security uplift and explicit recovery/change decisions.
