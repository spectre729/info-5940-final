# Application Design plan

Status: Component plan and asynchronous scan contract approved via A/A answers; generated design approved in chat. Execution plan is approved. Design remains within the accepted single-user local FastAPI application and six MVP features; this is not authorization to implement code.

## Proposed component boundaries

Use one modular local application rather than independent product microservices. Separate responsibilities behind typed interfaces so tests can replace providers and storage. One process/worker hosts web handlers, application services and scheduled/background scan orchestration; security/log collection boundaries may require separately isolated local facilities at NFR/Infrastructure Design. Do not claim all security controls can run under one app principal.

| Component | Responsibility and boundaries |
|---|---|
| Web interface | Render Jinja screens and validated JSON endpoints; enforce access/CSRF checks; return job/status views rather than expose providers directly. |
| Access and security boundary | Authorize the one local principal, validate sessions and permissions; provide policy ports for secrets, encryption and audit. Exact identity/key/HTTPS mechanisms remain NFR Design work. |
| Profile service | Import resumes/pasted input, propose source-linked claims, apply user confirmation/corrections and maintain immutable confirmed profile versions. |
| Source adapters | Normalize Adzuna/USAJOBS responses and user-pasted/fixture listing evidence. Fixed allowed hosts, typed requests/results, no automatic LinkedIn fetching. |
| Discovery coordinator | Shared scheduled/manual/catch-up scan entry point, locking, partial-success tracking, normalization and freshness/dedup orchestration. |
| Model gateway and evidence validator | Bounded provider calls and structured parsing; verify claim/listing references and approved tool contracts. The model may choose only supported retrieval tools within coordinator limits. |
| Recommendation and shortlist service | Explain accepted candidate matches, preserve user status, and expose evidence/unknowns; no invented eligibility or application decisions. |
| Bullet arrangement service | Return a unique ordered subset of existing confirmed bullet IDs and save only an accepted proposal; no new text generation. |
| Delivery service | Persist/show scan results and optionally send the same result set to the opted-in configured recipient; track failure separately from scan success. |
| Repository and local data boundary | Transactional profile/listing/status/run/arrangement records; storage and key-management ports enforce accepted encryption boundaries. No raw provider SQL in routes. |
| Recovery and observability boundary | Backup/restore/status and protected structured audit interfaces. Application writes events through a boundary without edit/delete privileges to its audit history. |

No final component IDs, filenames, schemas, libraries or deployment services are fixed by this proposal. Application Design will define interfaces, trust/dependency boundaries and high-level orchestration. Functional Design later defines detailed data models, algorithm rules and properties; NFR/Infrastructure Design selects secure mechanisms.

## Design contracts to document

- Typed immutable IDs and version references for confirmed claims, source evidence, profiles, listings, scans, delivery attempts and arrangements.
- Commands/results with explicit validation, unauthorized, conflict, timeout, rate-limited, unavailable and partial-success outcomes.
- No raw secrets/resume text in generic logs; audit version references rather than duplicate private payloads.
- Local calls through service/repository ports; external calls only through bounded gateway/adapter interfaces.
- Profile-version capture at scan start; do not mix changed/unconfirmed claims into an in-flight explanation.
- Side effects and transaction ownership for confirmation, save/hide, arrangement acceptance, deletion, scan completion, backup and delivery.
- Clear distinction between persisted successful listing retrieval and optional failed explanation/email.
- User-triggered writes require authentication, authorization, validation and user intent; source/model output cannot initiate unauthorized actions.

## Question 1: Component organization and design plan

May we use the component proposal and artifact-generation plan here as the high-level design approach? It preserves the accepted one-local-app deployment while separating services, typed interfaces and security/trust boundaries. Exact security mechanisms remain explicit design-stage work, not a relaxed requirement.

A) Approve this proposed organization and design plan, using the scan contract selected in Question 2.

B) Request revisions to the component boundaries or plan (specify changes within the approved requirements).

C) Other (describe after the answer tag).

[Answer]: A

## Question 2: User-initiated scan contract

How should the web app respond when a user starts a scan? Both choices retain four-hour/manual/catch-up triggers, one shared scan lock, saved results on restart and bounded provider calls. A running scan must be visible and a stopped process must not leave a permanently running status.

A) Return a persisted scan ID promptly, run the bounded work in the local process, and let the UI poll its status/results. If a scan is already active, return that scan rather than queue another. Interrupted runs become interrupted on restart, and recovery follows the existing catch-up policy (recommended for slow provider calls).

B) Keep the initiating HTTP request open until the bounded scan finishes, with clear running/timeout feedback and the same shared lock. Persist status so interruption can still be detected; accept that the browser request may wait through retrieval and model calls.

C) Other (describe completion/status/cancellation expectations after the answer tag).

[Answer]: A

## Execution checklist

- [x] Load approved requirements, personas/stories, inputs, execution plan and enabled extension obligations.
- [x] Evaluate component, method, service, dependency and pattern categories; identify the remaining scan-contract decision.
- [x] Propose component boundaries, typed contracts and artifact plan with embedded questions.
- [x] Receive both answers and analyze ambiguity/conflicts.
- [x] Resolve any ambiguity and record design-plan decision.
- [x] Generate application-design/components.md with component purpose, responsibilities, interfaces, requirement/story coverage and local workload criticality/dependency impacts.
- [x] Generate application-design/component-methods.md with typed method signatures, inputs/outputs and error contracts; detailed business rules deferred to Functional Design.
- [x] Generate application-design/services.md with orchestration, transaction/side-effect boundaries and main/partial/failure/user-review flows.
- [x] Generate application-design/component-dependency.md with dependency matrix, communication/trust boundaries and validated data-flow diagrams plus text alternatives.
- [x] Generate application-design/application-design.md consolidating the above, decisions, all FR/NFR/MVP/story coverage and deferred NFR/Infrastructure decisions.
- [x] Generate per-rule extension compliance review; require all applicable high-level obligations to have design ownership without claiming implemented controls.
- [x] Validate method/type/component references, coverage, dependency consistency and Markdown/diagrams before writing; update progress in this interaction.
- [x] Present generated design for explicit approval before Units Generation.
- [x] Record artifact approval and complete Application Design only after user review.

## Extension handling

Carry every approved security/recovery/PBT obligation to a named component/interface and later verification gate. Authentication/authorization, encrypted storage/transport, protected centralized logs, secrets, validation and safe failure must have owners now. Approved Backup and Restore retains RTO 4 hours/RPO 24 hours; the design defines logical snapshot/restore interactions without silently selecting retention or key recovery mechanisms. No production cloud zones, load balancer or autoscaling is introduced.

Resiliency CI/rollback/deployment-style/incident and experiment decisions remain user prompts at the permitted NFR Design stage. PBT-01 per-unit property analysis is performed in Functional Design, framework selection in NFR Requirements, and generated test configuration/verification during Construction. The component contracts must preserve traceable IDs and deterministic seams for those later checks. Compliance here is design coverage, not runtime evidence.
