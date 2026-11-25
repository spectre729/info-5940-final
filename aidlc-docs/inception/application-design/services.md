# Services and orchestration

Status: High-level orchestration from approved plan, asynchronous scan contract selected. No runtime mechanisms implemented.

## S01: Profile preparation and confirmation

C01/C02 authenticate and validate import -> C03 registers evidence -> C06 extracts typed claims -> C03 flags conflict/unconfirmed claims -> C01 displays original source references -> user confirms/corrects -> C03/C10 atomically commit a new confirmed version with audit metadata via C12. Rejected/unconfirmed claims do not enter matching. Concurrent version edits fail with conflict. Private import content is bounded and never logged. Confirmation invalidates or explicitly marks old-version explanations.

## S02: Discovery and scan lifecycle

C01 authenticated POST, local four-hour timer and startup all call C05.request_scan. Under one lock, return active ID if a scan exists; otherwise persist a pending run and profile-version snapshot, then return its ID before background work. UI polls an authorized status read. A process stop is not a promise of durable background execution: pending/running rows are marked interrupted at startup. One initial/due catch-up follows the approved clock policy; do not resume an old task that could send stale mail.

C05 invokes C06 for bounded allowlisted tool intents; C05 validates intent/source/budget and dispatches C04. C04 normalizes real received evidence, including snippet/full-text distinctions. Pasted/fixture sources use the same evidence boundary but are explicitly labeled. C07 merges identities and preserves saved/hide statuses, applies freshness and known requirement constraints, then obtains validated explanations through C06. No worthwhile matches is a successful empty outcome.

The captured profile version remains fixed throughout a run. If the user changes it mid-run, store results as belonging to the older version and mark them outdated; never silently attach them to the new profile. Source success/failure is recorded independently; a failed source cannot advance its success watermark. A scan may finish partial with useful factual listings even when one source or explanation call fails.

C05 commits source facts/results/status separately from delivery. No provider HTTP is held inside a long DB transaction. Every path records safe terminal status and releases the shared lock. Exact overall scan budget and retry/backoff policy beyond accepted per-call bounds belong to Functional/NFR Design. Polling itself never triggers another scan.

## S03: Shortlist and evidence review

C01/C02 -> C07 reads authorized source/profile snapshots and renders freshness, gaps, unknown fields and provenance. Save/hide commands carry expected revision and update status through C10 with redacted audit events. Status and canonical identity survive refresh/restart. Viewing a role never marks it applied. Source/evidence views are authenticated, escaped, local or supported links; a source URL is not permission to fetch it.

## S04: Selected-job bullet arrangement

User selects listing -> C08 loads confirmed profile/listing -> C06 proposes bullet IDs -> C08 verifies unique ordered subset and renders original confirmed text. Proposal has captured version/expiry state. Accept revalidates version and saves only the arrangement, not rewritten claim text. Reject does not mutate profile. If source claims were changed/deleted, proposal is stale and must be regenerated/reviewed.

## S05: Delivery

Results are already persisted for in-app use before C09 considers mail. C09 checks server running, valid recipient and explicit current consent; model/tool content cannot choose a destination. Delivery stores attempt/status separate from scan/source success. A user disabling email prevents later sends not already handed to SMTP. An ambiguous SMTP outcome is recorded as uncertain and not blindly retried after restart, avoiding a false exactly-once guarantee. Detailed bounded retry/send locking is Functional Design work. SMTP failure preserves in-app results; closed app sends nothing.

## S06: Access, safe errors and audited changes

C02 provides local-principal authentication/authorization to every resource route and service mutation, including scan/evidence/deletion/recovery. Security policies belong in dedicated modules, not templates. C01 handles request-level CSRF, size/format bounds, escaped HTML and required HTTPS/security-header policy; C10 uses parameterized queries and encryption ports. C06/C04 output is untrusted and cannot bypass these checks.

The logical audit protocol prepares a redacted event/outbox intent with a data change and obtains a durable collector receipt before treating a security-critical change as successfully complete. Exact transaction/collector failure reconciliation must be defined and tested in NFR/Functional Design; do not claim two-store atomicity. If protected logging is unavailable, fail closed for critical writes and offer only authorized safe reads. Collector runs with distinct permissions so app credentials cannot delete/edit audit records. No raw resume, secret, recipient or private listing payload is emitted into logs.

Misuse scenarios: a malicious listing requests email to another address; a resume injects instructions to invent qualifications; a browser requests another object's ID; a forged/expired session submits a write. In every case typed permissions, validation, captured evidence IDs and explicit user consent block the action, with redacted failure audit/alerts.

## S07: Backup, restore and deletion

C11 schedules encrypted consistent backups via C10 snapshot port, preserving manifests, required uploads/evidence and key references. The accepted goal is at most 24 hours of active-use state loss; backup schedule/retention and post-closure behavior are selected during NFR Design, not inferred as a promise of a running background daemon. A backup is successful only after encrypted artifact integrity checks. Failures appear in C12 status.

Restore enters maintenance mode, verifies keys and backup integrity, restores data, applies deletion generation/tombstones, checks profile/status consistency and performs an authorized smoke check before reopening. If checks fail retain the failed state for diagnosis without exposing private content; report safe failure. Record restore/failback and user communication steps; demonstrate RTO within 4 hours in Construction. Deletion must cover associated current data and disclose backup retention/expiry, with safeguards so restoration does not silently resurrect deleted profiles. Protected audit retention uses non-content IDs, not a second raw-data copy.

## S08: Observability and repeatable evaluation

C12 records structured correlation IDs, metrics and source/scan/delivery/backup states through a centralized protected collector. UI status/alerts show failures and last success. Health checks for local critical dependencies do not perform uncontrolled paid model calls. One process does not require distributed tracing; request/scan IDs correlate external operations.

All provider, clock, repository, SMTP, key and audit ports support deterministic doubles. Example fixtures demonstrate complete journeys; per-unit Functional Design identifies PBT invariants and stateful models; NFR Requirements selects framework; Construction configures shrinking/replay and CI. Generated tests do not claim real-model relevance or universal factual grounding.
