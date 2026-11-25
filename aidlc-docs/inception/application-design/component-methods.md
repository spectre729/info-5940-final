# Component methods and contracts

Status: Logical typed interface specification; not executable Python. Detailed validation bounds, state-machine rules, persistence schemas and per-unit properties belong to Functional/NFR Design.

## Shared vocabulary

| Type | High-level fields / constraints |
|---|---|
| Principal | Authenticated local identity and server-validated authorization context; never supplied as trusted input by a browser/model. |
| Result[T] | Success value or typed error: validation, unauthorized, forbidden, not_found, conflict, timeout, rate_limited, unavailable, partial. User-facing errors are safe; diagnostics are redacted. |
| SourceRef / Evidence | Immutable source ID, source kind, original text reference/span, URL or local evidence link, retrieved time and published-time precision. |
| Claim / ProfileVersion | Claim ID, original text, source IDs, review status; confirmed version ID with confirmed claims and preferences. |
| Listing | Stable local ID, canonical source identity, title/employer/location, actual received text, evidence and explicit unknown/date fields. |
| ScanRun / ScanReceipt | Run ID, trigger, captured profile version, lifecycle, per-source outcomes and timestamps; receipt is active/new plus status URL. |
| Explanation | Listing ID, captured profile version, confirmed claim IDs and listing spans, gaps/unknowns, validation status. |
| ArrangementProposal | Proposal ID, listing/version IDs, ordered unique confirmed bullet IDs and source refs; no new text. |
| DeliveryAttempt | Run ID, configured-recipient reference, consent version, status and attempt ID; no sensitive values in generic logs. |
| BackupManifest | Snapshot/version IDs, encryption-key reference, integrity metadata, time and deletion-generation marker; never raw key material. |
| AuditEvent | Actor/request/run IDs, action, timestamp, object/version references, before/after metadata excluding private text and secrets. |

IDs are distinct domain types, not interchangeable strings. All public methods require authenticated/authorized context or a constrained scheduler/service identity established by the app. IDs must be checked for ownership even in a single-user deployment. Ports return immutable values; storage mutation occurs only through a unit of work.

## Methods by component

| Owner | Signature | Contract / effects |
|---|---|---|
| C01 | start_scan(request: ScanCommand, context: RequestContext) -> Result[ScanReceipt] | POST /api/scans validates auth/CSRF and delegates. New scan returns 202 with persisted ID/status URL; active scan returns 200 with that ID, not another queue entry. |
| C01 | scan_view(scan_id: ScanId, context: RequestContext) -> Result[ScanView] | GET /api/scans/{id} authorizes ownership; pending/running/partial/succeeded/failed/interrupted status and safe results; no side effects. |
| C01 | render_profile / render_shortlist(context: RequestContext) -> Result[HtmlView] | Escaped accessible views; approved security headers; authorized local evidence URLs. |
| C02 | authenticate(session: SessionReference) -> Result[Principal] | Validate expiry/invalidation and reject unauthorized sessions; exact session mechanism later. |
| C02 | authorize(principal: Principal, action: Action, resource: ResourceRef) -> Result[AuthorizedContext] | Deny default; ownership/function checks, no reliance on UI hiding. |
| C02 | secret_ref(purpose: AllowedPurpose) -> Result[SecretHandle] | Scoped access for permitted adapters, no plaintext serialization/logging; managed by secure configuration. |
| C03 | propose_profile(inputs: ImportBatch, context: AuthorizedContext) -> Result[ProfileDraft] | Extract source-linked claims and mark conflicts; no confirmed mutation. |
| C03 | confirm_profile(draft_id: DraftId, edits: ReviewDecisions, expected_version: VersionId, context: AuthorizedContext) -> Result[ProfileVersion] | Atomically save confirmed version and invalidate/mark prior explanations; optimistic conflict returns conflict. |
| C03 | confirmed_profile(context: AuthorizedContext) -> Result[ProfileVersion] | Return current confirmed immutable snapshot for capture at scan start. |
| C03 | delete_profile(expected_version: VersionId, context: AuthorizedContext) -> Result[DeletionReceipt] | Atomically remove dependent private records and record deletion generation; backup treatment disclosed and applied on restore. |
| C04 | search(query: ValidatedSearch, source: SupportedSource, budget: CallBudget) -> Result[SourceBatch] | Adzuna/USAJOBS only, source credentials resolved outside input; bounded HTTP, source-specific failure. |
| C04 | ingest_pasted(text: BoundedText, url: Optional[SourceUrl], context: AuthorizedContext) -> Result[EvidenceListing] | Store supplied text; URL is attribution, not instruction to fetch. |
| C04 | replay_fixture(fixture_id: FixtureId) -> Result[SourceBatch] | Explicit synthetic/demo provenance. |
| C05 | request_scan(trigger: Trigger, context: AuthorizedContext) -> Result[ScanReceipt] | Atomically join active run or create pending run; capture profile version; submit bounded local work. |
| C05 | execute_scan(run_id: ScanId, budget: ScanBudget) -> Result[ScanOutcome] | Transition running, dispatch allowlisted intents, collect per-source outcomes, stage validated results and schedule delivery; cleanup releases lock. |
| C05 | recover_startup(clock: Clock) -> Result[RecoverySummary] | Mark persisted pending/running work interrupted, load saved results, initiate one initial/due catch-up under lock. |
| C06 | extract(inputs: ImportEvidence, budget: CallBudget) -> Result[ClaimProposal] | Bounded provider result, structural and provenance validation. |
| C06 | plan_tools(profile: ProfileVersion, context: SearchContext, budget: CallBudget) -> Result[List[ToolIntent]] | Allowlisted typed intents only; coordinator owns actual tools and budgets. |
| C06 | explain(profile: ProfileVersion, listing: Listing, budget: CallBudget) -> Result[ExplanationProposal] | Propose evidence-linked fit/gaps; validate references, not pretend to prove semantic truth solely via IDs. |
| C06 | arrange(profile: ProfileVersion, listing: Listing, budget: CallBudget) -> Result[ArrangementProposal] | Ordered subset of confirmed IDs; original text rendered by app, not generated text. |
| C07 | normalize_and_merge(batch: SourceBatch, context: AuthorizedContext) -> Result[List[Listing]] | Preserve actual evidence and source facts, deduplicate transactionally without losing statuses. |
| C07 | evaluate(profile: ProfileVersion, listings: List[Listing], budget: ScanBudget) -> Result[RecommendationBatch] | Code applies freshness/known constraints; validated explanations reference captured profile, no quota padding. |
| C07 | set_status(listing_id: ListingId, status: UserStatus, expected_revision: Revision, context: AuthorizedContext) -> Result[ListingView] | Explicit save/hide or supported status update; no application inferred from view. |
| C07 | shortlist(query: ShortlistQuery, context: AuthorizedContext) -> Result[ShortlistView] | Source labels, profile version, gaps, freshness and saved statuses. |
| C08 | propose(listing_id: ListingId, context: AuthorizedContext) -> Result[ArrangementProposal] | Retrieve current confirmed profile and actual listing; validate model-proposed ID subset. |
| C08 | decide(proposal_id: ProposalId, decision: AcceptOrReject, expected_version: VersionId, context: AuthorizedContext) -> Result[ArrangementDecision] | Reject leaves profile unchanged; stale version returns conflict; accept stores arrangement separately without rewriting claims. |
| C09 | configure_delivery(settings: DeliverySettings, context: AuthorizedContext) -> Result[ConsentVersion] | User only; validate recipient, explicit opt-in, audit consent metadata. |
| C09 | deliver(run_id: ScanId, context: ServiceContext) -> Result[DeliveryAttempt] | Persist in-app view first; recheck opt-in and fixed recipient before SMTP; track ambiguity/failure without claiming exactly-once mail delivery. |
| C10 | transaction(operation: ValidatedOperation, context: AuthorizedContext) -> Result[CommittedChange] | Parameterized repository operations, encryption at rest, version checks and redacted audit/outbox intent; no network/provider calls held inside DB transaction. |
| C10 | snapshot(context: RecoveryContext) -> Result[ConsistentSnapshot] | Consistent database plus upload/evidence manifest; no naive copy of an actively written SQLite file. |
| C10 | restore(snapshot: VerifiedSnapshot, deletion_generation: Generation, context: RecoveryContext) -> Result[RestoreReceipt] | Maintenance-mode transactional restore, preserve post-snapshot deletion policy, validate before reopening writes. |
| C11 | backup_due(clock: Clock, context: RecoveryContext) -> Result[BackupReceipt] | Scheduled encrypted backup meeting 24-hour RPO during active use; update inventory only after integrity checks. |
| C11 | restore(backup_id: BackupId, context: RecoveryContext) -> Result[RecoveryReport] | Key/snapshot verification, maintenance mode, restore, deletion handling and saved-state validation under 4-hour target; no false success. |
| C12 | emit(event: RedactedEvent, context: AuditWriterContext) -> Result[AuditReceipt] | Append to protected collector; app has no update/delete capability. Audit write failure prevents unaudited critical mutation per later failure policy. |
| C12 | health(context: AuthorizedContext) -> Result[HealthView] | Process/DB/scan/backup/delivery health, last success and alert states without secrets. |

## Boundary rules

All ID-based fetches enforce ownership. Source fetches use 15-second timeout, model calls 45 seconds, at most one transient retry respecting provider guidance. Overall tool rounds, payload sizes, polling cadence and per-store/SMTP limits are explicit Functional/NFR Design outputs, not unlimited loops. Sessions, secret encryption keys and provider instances do not cross into generic DTOs. Missing facts remain unknown. Model proposal schemas are not substitutes for deterministic validation or factual-evidence review.
