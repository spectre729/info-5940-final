# User stories

Status: Generated under the approved journey-based plan; approved in chat; see audit.md. Personas P-01 and P-02 are defined in personas.md. Each story applies to both unless a scenario explicitly describes a context. Requirements remain authoritative; these stories do not add excluded features or choose deferred technical mechanisms.

All stories use a standard local job-seeker persona (P-01 or P-02). Tests and outcomes below are acceptance specifications, not assertions that software already exists. Dependencies indicate reusable capabilities, not an implementation sequence or sprint plan.

## Set up my profile

### US-01: Import my background

As a student or recent graduate (P-01/P-02), I want to bring several resumes and pasted text into one review so I do not re-enter my experience.

- Requirements: FR-01; MVP-01.
- Personas: P-01, P-02.
- Dependencies: None.

Acceptance criteria:

1. **Given** two text-bearing resumes, pasted profile text and preferences, **when** I submit valid inputs, **then** the app proposes extracted claims with a source reference for each and does not use them for matching yet.
2. **Given** an unreadable scanned PDF or invalid/oversized input, **when** I attempt import, **then** the app gives a safe actionable error and paste alternative without inventing claims or exposing internal paths.

### US-02: Confirm and correct my profile

As a student or recent graduate (P-01/P-02), I want to confirm or correct each claim so matching reflects experience I actually have.

- Requirements: FR-01; FR-02; MVP-01.
- Personas: P-01, P-02.
- Dependencies: US-01.

Acceptance criteria:

1. **Given** proposed claims and a contradiction across resumes, **when** I review the profile, **then** conflicting claims are flagged and remain unresolved until I choose or correct them.
2. **Given** one corrected claim and one rejected claim, **when** I confirm the profile and request matching, **then** only the confirmed corrected values are used; rejected/unconfirmed claims are excluded and provenance is preserved.

### US-03: Update my confirmed background

As a student or recent graduate (P-01/P-02), I want to update my background without mistaking old explanations for current advice.

- Requirements: FR-02; MVP-01.
- Personas: P-01, P-02.
- Dependencies: US-02.

Acceptance criteria:

1. **Given** an existing explanation tied to profile version 1, **when** I confirm an edited profile as version 2, **then** the previous explanation is invalidated or explicitly marked as based on version 1.
2. **Given** an edit not yet confirmed, **when** I leave the review without acceptance, **then** the last confirmed profile remains authoritative; no proposed claim silently replaces it.

## Discover opportunities

### US-04: Retrieve supported opportunities

As a student or recent graduate (P-01/P-02), I want to search supported sources so I can inspect recent opportunities without manually opening every board.

- Requirements: FR-03; NFR-06; MVP-02.
- Personas: P-01, P-02.
- Dependencies: US-02.

Acceptance criteria:

1. **Given** a confirmed profile and configured supported source, **when** I run a retrieval, **then** returned listings retain source IDs, actual received text, source links, fetch time and supplied posting times; Adzuna snippets are not presented as full descriptions.
2. **Given** text containing instructions to change tools or destinations, **when** the agent examines it, **then** the app treats it as untrusted evidence and allows only validated tools and fixed API hosts; it does not connect to LinkedIn or fetch arbitrary URLs.

### US-05: Review a job I paste

As a student or recent graduate (P-01/P-02), I want to add a job description from another board so it can be compared with my profile.

- Requirements: FR-03; MVP-02.
- Personas: P-01, P-02.
- Dependencies: US-02.

Acceptance criteria:

1. **Given** a pasted LinkedIn or other job description with optional URL, **when** I add it, **then** the app stores the supplied text and links to that source or local evidence when no URL exists.
2. **Given** only an arbitrary URL with no job text, **when** I submit it, **then** the app requests job text rather than initiating unsupported scraping or inventing a description.

### US-06: Refresh on demand or schedule

As a student or recent graduate (P-01/P-02), I want to refresh opportunities while the app runs so new listings arrive without repeated manual screening.

- Requirements: FR-04; NFR-02; MVP-02.
- Personas: P-01, P-02.
- Dependencies: US-04.

Acceptance criteria:

1. **Given** the app is running and a scan is due, **when** a four-hour timer or Scan now fires, **then** one scan runs through a shared lock; overlapping triggers do not start duplicate scans.
2. **Given** the app is stopped, **when** a scheduled time passes, **then** no scan or email occurs.
3. **Given** no successful scan exists, or the last success is over four hours old, **when** I launch the app, **then** saved results appear when available and one initial/catch-up scan runs; repeated startup triggers do not create duplicate concurrent scans.

### US-07: Understand listing freshness

As a student or recent graduate (P-01/P-02), I want to see trustworthy freshness labels so I can prioritize recent listings.

- Requirements: FR-05; MVP-02.
- Personas: P-01, P-02.
- Dependencies: US-04 or US-05.

Acceptance criteria:

1. **Given** an exact source timestamp aged between zero and 72 hours inclusive, **when** I view results, **then** the listing is labeled fresh and ordered before older listings.
2. **Given** a future, missing, ambiguous or insufficiently precise timestamp, **when** I view results, **then** freshness is unknown unless reliable evidence resolves it; fetch time is not substituted.
3. **Given** a timestamp 72 hours and one second old, **when** I view results, **then** the listing is older, and missing eligibility or work arrangement is not described as satisfied.

## Understand and decide

### US-08: Understand fit and gaps

As a student or recent graduate (P-01/P-02), I want to read an explanation grounded in my profile and the listing so I can judge whether applying is worthwhile.

- Requirements: FR-06; NFR-06; MVP-03.
- Personas: P-01, P-02.
- Dependencies: US-02; US-04 or US-05.

Acceptance criteria:

1. **Given** a listing and confirmed profile, **when** the model proposes an explanation, **then** each accepted explanation references at least one confirmed claim and one actual listing detail, with missing qualifications and uncertainty stated.
2. **Given** a fabricated claim ID, unsupported evidence or attempted instruction injection, **when** the explanation is validated, **then** the output is rejected or shown unavailable instead of displaying invented experience, dates or eligibility.
3. **Given** no worthwhile matches, **when** I review the result, **then** the app permits an empty shortlist without filling a quota.

### US-09: Save or hide without repeat recommendations

As a student or recent graduate (P-01/P-02), I want to save promising roles and hide others so later scans preserve my decisions.

- Requirements: FR-07; MVP-04.
- Personas: P-01, P-02.
- Dependencies: US-04 or US-05.

Acceptance criteria:

1. **Given** a listing I save or hide, **when** it reappears in a later scan or after restart, **then** my status is preserved and it is not presented as new.
2. **Given** two listings with the same source/requisition ID or fallback normalized employer/title/location/URL, **when** results are merged, **then** one listing is shown and existing saved/hidden status is retained.
3. **Given** a viewed listing, **when** I have not marked it applied, **then** the app does not infer an application; represented applied/rejected statuses survive refresh.

## Receive results

### US-10: Read results in the app

As a student or recent graduate (P-01/P-02), I want to read the latest results and their status in the app so I can act without email.

- Requirements: FR-08; NFR-05; MVP-05.
- Personas: P-01, P-02.
- Dependencies: US-06.

Acceptance criteria:

1. **Given** default delivery settings, **when** a scan completes, **then** results appear in the app and no email is sent.
2. **Given** an empty, partial or failed scan, **when** I review the result screen, **then** clear accessible status labels distinguish no matches, stale data and errors without relying only on color.

### US-11: Opt into email delivery

As a student or recent graduate (P-01/P-02), I want to choose email delivery to my configured address so I can receive results through my preferred channel.

- Requirements: FR-08; NFR-02; MVP-05.
- Personas: P-01, P-02.
- Dependencies: US-10.

Acceptance criteria:

1. **Given** email is off or my address is invalid, **when** a scan completes, **then** the app sends no email and reports configuration/validation feedback safely.
2. **Given** I explicitly enable email to a valid configured address and the app remains running, **when** a scan finishes, **then** the same result set is sent to that address using encrypted SMTP, not to a model-selected recipient.
3. **Given** SMTP fails or I disable delivery, **when** delivery is attempted or future scans complete, **then** in-app results remain intact, failure is not called success, and disabled email sends nothing; no email is sent while the app is closed.

## Prepare for a selected role

### US-12: Review existing resume bullets for one job

As a student or recent graduate (P-01/P-02), I want to choose which existing resume bullets to emphasize so my experience is presented for a selected role.

- Requirements: FR-09; MVP-06.
- Personas: P-01, P-02.
- Dependencies: US-02; US-08.

Acceptance criteria:

1. **Given** a selected listing and confirmed original bullets, **when** I request an arrangement, **then** the proposal contains only a unique ordered subset of confirmed bullet IDs with original text and provenance.
2. **Given** an invented, duplicate or unconfirmed bullet ID, **when** a proposal is validated, **then** it is rejected without inventing text, skills, employers, dates or metrics.
3. **Given** a valid proposal, **when** I accept or reject it, **then** acceptance saves the arrangement; rejection leaves my profile unchanged and no proposal is silently saved.

## Control my data

### US-13: Inspect and remove personal data

As a student or recent graduate (P-01/P-02), I want to inspect sources and delete local profile data so I control what the product retains.

- Requirements: FR-10; SEC-REQ-08.
- Personas: P-01, P-02.
- Dependencies: US-01; US-09.

Acceptance criteria:

1. **Given** an extracted claim or recommendation, **when** I open its source, **then** I can inspect the associated evidence rather than an unsupported assertion.
2. **Given** my stored profile/uploads and associated recommendations, **when** I explicitly request deletion, **then** the specified local data is removed and stale explanations are no longer used; the UI discloses backup retention/deletion limitations from the approved design.
3. **Given** a critical data change, **when** the app records its audit event, **then** actor, time and before/after version references are retained without copying private text or secrets into the log.

## Use the app safely

### US-14: Protect my local session and stored data

As a student or recent graduate (P-01/P-02), I want to control access to my local profile so a local installation does not expose it to unauthenticated requests.

- Requirements: SEC-REQ-01; SEC-REQ-03; SEC-REQ-04; SEC-REQ-05; SECURITY-01; SECURITY-04; SECURITY-08; SECURITY-12.
- Personas: P-01, P-02.
- Dependencies: None.

Acceptance criteria:

1. **Given** an unauthenticated, expired or unauthorized request for a protected resource, **when** the request is handled, **then** access is denied server-side; ownership and function permissions are checked and CORS is restricted.
2. **Given** a browser write request without valid cross-site protection, **when** it reaches the server, **then** the write is rejected; authenticated sessions expire, invalidate on logout and use Secure/HttpOnly/SameSite protections.
3. **Given** profile persistence or network transmission, **when** the app stores or transfers data, **then** stores and backups use managed/customer-controlled encryption keys and network paths use TLS 1.2+ including local HTTPS, with the required CSP/HSTS/nosniff/framing/referrer headers.
4. **Given** a chosen authentication mechanism, **when** credentials and sessions are provisioned, **then** design-selected credential controls meet SEC-REQ-05, including conditional password/admin-MFA rules; secrets are not hardcoded or committed.

## Recover from errors

### US-15: Keep useful results when a dependency fails

As a student or recent graduate (P-01/P-02), I want to retain safe usable results when retrieval, models or delivery fail so a transient outage does not erase my work.

- Requirements: FR-06; NFR-02; NFR-03; SEC-REQ-06; SEC-REQ-08; RESILIENCY-10.
- Personas: P-01, P-02.
- Dependencies: US-04; US-06.

Acceptance criteria:

1. **Given** a slow or throttled source/model, **when** the request exceeds configured bounds or returns retry guidance, **then** source requests use a 15-second limit and model calls 45 seconds with at most one transient retry, respecting provider intervals; resources and locks are released.
2. **Given** one source fails after earlier success, **when** the scan completes partially, **then** last successful results are preserved, failed-source success time is not falsely advanced, and stale/partial labels are visible.
3. **Given** the model or input validation fails, **when** I inspect factual listings, **then** facts remain available with explanation unavailable, safe generic errors reveal no stack trace, and failed transactions do not bypass validation/access controls.

### US-16: Restore saved work after local failure

As a student or recent graduate (P-01/P-02), I want to restore my saved profile and shortlist so a local failure does not require rebuilding everything.

- Requirements: NFR-04; RESILIENCY-02; RESILIENCY-11; RESILIENCY-12; RESILIENCY-13.
- Personas: P-01, P-02.
- Dependencies: US-02; US-09.

Acceptance criteria:

1. **Given** saved profile, shortlist and retained supporting files during active use, **when** scheduled backups run, **then** encrypted consistent backups meet a maximum 24-hour data-loss window; failures are surfaced instead of silently claiming protection.
2. **Given** a documented restore drill with the required backup and keys, **when** the local data store is lost, **then** the documented procedure restores service within four hours and validates data integrity and saved statuses.
3. **Given** the application is deliberately closed, **when** no uptime is promised, **then** recovery claims remain within the accepted active-use scope, and backup retention/key-recovery details follow the later approved design.

### US-17: Know whether a scan or backup needs attention

As a student or recent graduate (P-01/P-02), I want to see health and security/recovery alerts so I can distinguish working, stale and unsafe states.

- Requirements: NFR-08; SEC-REQ-02; SEC-REQ-07; SECURITY-03; SECURITY-09; SECURITY-14.
- Personas: P-01, P-02.
- Dependencies: US-06; US-14; US-16.

Acceptance criteria:

1. **Given** a scan, backup or access-control failure, **when** the event is recorded, **then** centralized protected structured logs include timestamp, level and correlation ID, with no secret or personal payload; security logs are retained at least 90 days and the app cannot edit/delete them.
2. **Given** repeated authentication failures or authorization denials, **when** monitoring handles the event, **then** a security alert and inspectable status appear through the design-selected mechanism.
3. **Given** the app exposes health/error information, **when** I view it, **then** health and operational status are available to the authorized local user without credentials, internal paths or debug details being disclosed.

## Evaluate the product

### US-18: Review a reproducible local demonstration

As a student or recent graduate (P-01/P-02), I want to review repeatable sample results so I can evaluate the workflow without confusing fixtures with live evidence.

- Requirements: NFR-01; NFR-05; NFR-07; NFR-09; SECURITY-10; SECURITY-13.
- Personas: P-01, P-02.
- Dependencies: US-01 through US-17 for full demonstration.

Acceptance criteria:

1. **Given** a teammate follows the approved local setup and locked dependencies, **when** the synthetic fixture demo runs, **then** it is clearly labeled replay and covers corrected claims, freshness boundaries, duplicates, unknown requirements, bullet rejection and dependency failures without live credentials.
2. **Given** the reviewer navigates the workflow by keyboard, **when** profile and shortlist controls are used, **then** controls are labeled, errors readable and statuses do not rely solely on color.
3. **Given** a change to data/runtime behavior is proposed, **when** the team reviews its GitHub PR, **then** cross-part review includes test evidence and rollback impact; dependency integrity/scanning and generated plus example tests are carried to Construction with no claimed live quality metric.

## INVEST review and scope

Stories describe distinct observable outcomes with mockable boundaries. Import/confirmation, retrieval/explanation, app/email delivery and proposed/accepted bullet arrangements are separated. Supporting security/recovery/evaluation stories are independently reviewable outcome slices; their technical controls will be decomposed into components/units at Application Design and Units Generation. Necessary dependencies are explicit rather than claiming every story is independently deployable. Exact estimates belong after design; no time estimates or sprint commitments are fabricated here.

Negotiability applies to UX and implementation within approved constraints, not to dropping consent, source evidence or enabled security obligations. Each story has concrete examples suitable for acceptance tests. Generated property tests complement them at Construction: serialization round-trips, freshness invariants, deduplication idempotence, confirmed-bullet subset validation and stateful save/hide/refresh behavior. These do not measure real-model relevance or prove factuality.

No networking, recruiter discovery, essay generation, automated new resume content, mailbox/calendar integration, multiple-user accounts or cloud deployment is added. An empty shortlist is a valid outcome. Live model/API access remains a validation risk rather than an observed capability.

## Requirement coverage

| Requirement | Stories |
|---|---|
| FR-01 | US-01, US-02, US-18 |
| FR-02 | US-02, US-03, US-06, US-11, US-15 |
| FR-03 | US-04, US-05, US-15 |
| FR-04 | US-06, US-16 |
| FR-05 | US-07, US-10, US-18 |
| FR-06 | US-04, US-08, US-15 |
| FR-07 | US-09, US-18 |
| FR-08 | US-10, US-11, US-17 |
| FR-09 | US-12, US-18 |
| FR-10 | US-13 |
| NFR-01 | US-18 |
| NFR-02 | US-06, US-11, US-15 |
| NFR-03 | US-15 |
| NFR-04 | US-16 |
| NFR-05 | US-10, US-18 |
| NFR-06 | US-04, US-08 |
| NFR-07 | US-18 |
| NFR-08 | US-17 |
| NFR-09 | US-18 |
| MVP-01 | US-01, US-02, US-03 |
| MVP-02 | US-04, US-05, US-06, US-07 |
| MVP-03 | US-08 |
| MVP-04 | US-09 |
| MVP-05 | US-10, US-11 |
| MVP-06 | US-12 |

## Extension review

See story-extension-compliance.md for the per-rule story-stage matrix. All three extensions remain enabled. No unresolved story-level finding is identified; architecture/runtime/test checks remain downstream gates, not implemented controls.
