# Components

Status: Generated from approved Application Design plan; approved in chat; see audit.md. Interfaces are logical contracts, not implemented modules. One product process/worker is retained; HTTPS, key custody, storage encryption and protected logging may use separate local facilities with distinct permissions. Detailed mechanisms are not silently chosen here.

## C01: Web interface

Authenticated HTML/JSON routes, schema validation, escaped views and CSRF/headers. Delegates commands to services; never issues raw SQL/provider calls. Polls persisted scan status.

- Coverage: FR-01..10; NFR-05; US-01..18.
- Dependencies: C02,C03,C05,C07,C08,C09,C11,C12.
- Workload classification/impact: Low business criticality; absence prevents local interaction but cannot submit applications.

## C02: Access and security boundary

Local principal/session validation, object/function authorization, secret/key references and transport/security policy ports. Deny by default; explicitly public bootstrap/health routes must be separately enumerated during NFR Design.

- Coverage: SEC-REQ-01/03/04/05/06/07; US-14.
- Dependencies: C10,C12.
- Workload classification/impact: Low business criticality, security-critical control: failure denies access rather than bypassing checks.

## C03: Profile service

Import proposals, extraction validation, claim provenance, conflict review, confirmation and immutable version references. Changes mark previous explanations outdated. Does not fabricate claims or select unresolved conflicts.

- Coverage: FR-01/02/10; MVP-01; US-01/02/03/13.
- Dependencies: C06,C10,C12.
- Workload classification/impact: Low; interruption delays profile setup. Confirmed claims remain persisted.

## C04: Source adapters

Normalized Adzuna/USAJOBS search ports, pasted text storage and explicit fixture replay. Retain actual text, provenance and date precision; no automatic arbitrary URL or LinkedIn fetch.

- Coverage: FR-03/05; MVP-02; US-04/05/07.
- Dependencies: None internally; external API and credential ports.
- Workload classification/impact: Low; each unavailable source yields partial results and source-specific status.

## C05: Discovery coordinator

Single lock and bounded shared scan entry point for timer/manual/startup. Persists run ID/status, captures profile version, dispatches approved tool requests, coordinates evidence normalization and matching, then schedules delivery.

- Coverage: FR-03/04/05; NFR-02/03; US-04/06/07/15.
- Dependencies: C03,C04,C06,C07,C09,C10,C12.
- Workload classification/impact: Low; interruption delays scans, not applications. Locks/unfinished runs recover explicitly.

## C06: Model gateway and evidence validator

Bounded profile/relevance/bullet calls with explicit provider configuration. Returns typed proposals, supported tool intents and evidence references; validates syntax and domain references before use. No authority to write profile/status or send mail.

- Coverage: FR-01/06/09; NFR-06; US-01/08/12/15.
- Dependencies: None internally; external model/credential ports.
- Workload classification/impact: Low; failure leaves source facts visible and explanation unavailable.

## C07: Recommendation and shortlist service

Freshness classification and deterministic eligibility/unknown handling; confirmed-profile fit explanations, persisted source evidence, canonical identity/dedup, save/hide transitions and evidence views.

- Coverage: FR-05/06/07; MVP-03/04; US-07/08/09.
- Dependencies: C06,C10,C12.
- Workload classification/impact: Low; failure retains last results and statuses; no unverified match implied.

## C08: Bullet arrangement service

Selected-job proposal of ordered unique confirmed IDs, original-text rendering and explicit acceptance/rejection. Stores accepted arrangement separately from canonical claim text.

- Coverage: FR-09; MVP-06; US-12.
- Dependencies: C06,C10,C12.
- Workload classification/impact: Low; unavailable suggestions do not block job review.

## C09: Delivery service

In-app result views and opted-in email to the fixed configured recipient. Consent snapshot and current opt-in checked before sending; delivery attempts tracked separately. No model-selected recipient or outreach.

- Coverage: FR-08; MVP-05; US-10/11.
- Dependencies: C10,C12; external SMTP/credential ports.
- Workload classification/impact: Low; SMTP outage preserves in-app results and visible delivery status.

## C10: Repository and local data boundary

Transactional repositories, immutable version IDs, listing/status/run/delivery records and unit-of-work protocol. Uses encryption/key-custody ports; plaintext SQLite is not a compliant default. Data deletion includes dependent records and backup-deletion markers.

- Coverage: FR-02/07/10; NFR-01/04; SEC-REQ-01/08; US-03/09/13/16.
- Dependencies: None internally; encrypted storage/key ports.
- Workload classification/impact: Low business criticality, integrity-sensitive; access/storage failure prevents writes and returns safe error.

## C11: Recovery service

Consistent encrypted snapshots, encrypted backup inventory, restore/validation and restart recovery. RTO 4 hours/RPO 24 hours; retention, cadence and key-recovery concrete decisions are NFR Design outputs. Applies deletion markers before restored data becomes visible.

- Coverage: NFR-04; RESILIENCY-11/12/13; US-16.
- Dependencies: C10,C12; backup/key ports.
- Workload classification/impact: Low; backup failure alerts user and prevents false protection claims; data-loss impact is explicit.

## C12: Observability and audit boundary

Structured redacted event writer, protected centralized collector port, metrics/health/status and security/backup failure signals. Collector permissions separate append from edit/delete; app cannot erase its audit trail.

- Coverage: NFR-08; SEC-REQ-02/08; US-13/17.
- Dependencies: None internally; separately protected collector/alert ports.
- Workload classification/impact: Low business criticality, audit-sensitive; failure policy separates prohibited unaudited critical changes from safe read-only views.

## External and trust boundaries

Browser input -> authenticated/validated C01/C02 -> services -> C10 data and C12 audit ports. Resumes, pasted job text, source API text and model proposals are untrusted. Only C04 performs source retrieval; C06 proposes tool intents but C05 validates and dispatches them. C09 alone can send result email after consent. Providers receive only the text required for the selected task. Secrets are injected as opaque references, not returned in domain objects or logs.

No cloud IAM, load balancer, CDN, production zones or multi-user account platform is introduced. Roles in README are team responsibilities, not application privileges.
