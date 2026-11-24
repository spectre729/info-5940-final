# Evidence-based specification of a personal job-search assistant

**As of:** November 19, 2026  
**Purpose:** Course-project requirements and scope analysis, not a claim that all described capabilities have been implemented.  
**Privacy:** Candidate details are generalized; personal contacts, correspondence, credentials, and private resume text are omitted.  
**Change control:** This review only read task definitions and recorded results. No tasks were created, edited, run, or deleted.

A note from dennis: I have something similar set up on ChatGPT, so this doc was made as a reference. 

## Evidence labels and method

- **[Confirmed — instruction]** An accessible saved task prompt explicitly requests the behavior. This is **not** evidence that execution succeeds.
- **[Confirmed — observed]** An accessible recorded task result or conversation/history shows the behavior or a user-reported action. Where the only evidence is a user report, it is called out.
- **[Confirmed — configuration]** An accessible automation record contains the setting, such as schedule, status, or timezone.
- **[Inferred]** A reasonable synthesis or design implication, not directly specified or demonstrated.
- **[Unknown]** No sufficiently reliable evidence is accessible. Do not treat this as evidence that a feature does not exist.

**Evidence available:** current request; saved user-context summary and recent-conversation excerpts; 12 automation definitions returned by a read-only automation listing (three active, plus nine inactive or one-off historical tasks); two complete latest-run outputs from November 19; and run metadata. The detailed run result of the job-scan task was **not readable**: the read-only query returned an error. Historical excerpts are not complete logs. This is **not** a code, database, or production-architecture audit. Tool descriptions indicate possible capabilities, but do not prove the job-search automations actually invoked each tool. The recorded task-output delivery field is `unknown`.

## 1. Problem and intended daily workflow

- **[Confirmed — user history]** The system assists a recent computer-science graduate searching for new-grad/early-career software engineering roles, with AI/ML roles secondary. It addresses the repeated effort of discovering recent, eligible, nonduplicative postings; prioritizing applications; finding appropriate networking contacts; and keeping recruiting obligations from falling through the cracks.
- **[Confirmed — instruction]** The job scan should periodically produce only genuinely worthwhile opportunities, including evidence about freshness, work arrangement, eligibility, fit, and an application link. The networking task should propose outreach and follow-ups. The recruiting monitor should surface unresolved actions and avoid repeating completed items.
- **[Inferred — intended daily workflow]** (1) Review new role recommendations; (2) verify fit and choose which to apply to; (3) tailor resume or answer questions with human review; (4) record submitted applications; (5) review networking drafts and manually approve/send outreach; (6) review assessments, interview invitations, and outstanding actions; (7) report completions or corrections so later recommendations do not repeat them. These steps are assembled from instructions and conversation rather than a single documented flowchart.
- **[Confirmed — observed]** Conversations show manual application decisions, short-answer drafting, tracker reconciliation requests, and user updates that an assessment/interview was completed or an invitation sent. A November 19 networking run generated five actions and stated **no outreach was sent and no tracker entries were modified**. A November 19 recruiting run identified four open actions and stated **no calendar events were added** because the known confirmed appointment was already present.
- **[Unknown]** Whether there is a single daily dashboard, automated write-back of all state, or a consistent end-to-end transaction from discovery to application submission.

## 2. Candidate information and conflicts

| Information | Evidence-backed description |
|---|---|
| Education and eligibility | **[Confirmed — saved context / instruction]** CS bachelor's degree and an expected December 2026 CS master's completion; U.S. citizenship was reported in a prior application context. The role scanner explicitly checks graduation eligibility. This is user-provided context, not an independently verified credential. |
| Skills | **[Confirmed — saved context]** Python, C/C++, JavaScript/React, SQL, cloud/backend services, PyTorch and ML tools, mobile and embedded work, testing/APIs. The live representation or ranking weights are **[Unknown]**. |
| Projects and work | **[Confirmed — saved context]** Experience categories include cloud/backend API and scraping infrastructure, full-stack/mobile work, ML research with measurable speedups, embedded development, and independent automation projects. Private bullet-level resume content is omitted here. |
| Interests | **[Confirmed — saved context]** SWE primarily; ML/AI and related systems secondarily; interest in backend/infrastructure and applied AI. |
| Locations and work style | **[Confirmed — instruction]** Prefer major U.S. cities, especially New York City and the San Francisco Bay Area; require explicit on-site or hybrid arrangements; exclude fully remote and remote-only listings. |
| Employer/role preferences | **[Confirmed — instruction]** Big technology employers and strong smaller companies; new-grad or early-career fit. No mandatory employer whitelist is visible. |
| History | **[Confirmed — saved context]** Applications, interviews, assessments, referrals, outreach statuses, and closures have been recounted across chats and a named spreadsheet-style job/network tracker. |

- **[Confirmed — saved context]** Multiple resume versions have existed: a general SWE resume, role-tailored versions, and subsequent revisions that changed project emphasis. The job-scan prompt says to use the **latest resume** and give bullet-specific tailoring guidance for high-value roles.
- **[Unknown]** How a run locates the latest resume, distinguishes a canonical version from role-specific versions, parses PDFs/LaTeX, resolves conflicting graduation dates or skills, or chooses among discrepant tracker and memory records. No version precedence, timestamps, formal conflict-resolution policy, or resume repository schema was provided.
- **[Inferred — design requirement, not existing behavior]** A rebuilt system should maintain one user-approved canonical profile, explicit resume-version IDs, role-specific variant links, source/timestamp for each claim, and a `needs_review` status on conflicts. Never silently merge contradictory claims or invent skills.

## 3. Scheduled task definitions and delivery

**[Confirmed — configuration]** All three core tasks were enabled when inspected, and all specify `America/New_York` as their default timezone. The table reflects the saved schedule recurrence, **not** a guarantee that execution occurs at exactly those wall-clock times.

| Task | Saved cadence and mode | Trigger / output behavior | Latest accessible evidence |
|---|---|---|---|
| Fresh New-Grad Role Scan | Every 4 hours (`RRULE:FREQ=HOURLY;BYMINUTE=0;INTERVAL=4`); exact_schedule | Scheduled scan; prompt asks for useful role shortlist even if shorter than a quota | Run timestamp exists on Nov 19; detailed run output inaccessible, so its result is **[Unknown]** |
| Daily Networking Plan | Every 6 hours (`RRULE:FREQ=HOURLY;INTERVAL=6;BYMINUTE=0`); exact_schedule, despite its “Daily” title | Scheduled suggestions and follow-ups; human approval required before outreach | **[Confirmed — observed]** Completed Nov 19 run with five proposed actions; explicitly no outreach or tracker changes |
| Recruiting Action Watch | Daily, approximately 9:33 a.m. Eastern in current display (`RRULE:FREQ=DAILY;BYHOUR=9`, with its saved start-time minutes); condition_watch | Checks for unresolved recruiting actions; no notification if none; conditional calendar creation for confirmed timed appointments | **[Confirmed — observed]** Completed Nov 19 run with four actions; checked calendar; added no event |

**[Confirmed — configuration]** The first and third task names accurately describe their focus; the second is not literally once daily. Some additional specialized employer watches, one-off reminders, and reply watches existed but were inactive. Those are ancillary rather than core capabilities.

**[Confirmed — instruction]** Data-source requests include the job application tracker and recent confirmation evidence when available; networking history, LinkedIn context and professional-email availability; and connected Gmail plus Google Calendar for recruiting action checks. **[Confirmed — observed]** The networking run explicitly reported checking connected Gmail messages and sent mail, while noting that LinkedIn message content and invitation statuses were independently unverified. The recruiting run explicitly reported checking two connected Gmail accounts, later correspondence, and Google Calendar. **[Unknown]** Which search engines, scraping implementations, job APIs, storage systems, or browser actions the job-scan runs actually used; detailed per-run tool traces are unavailable.

**[Confirmed — configuration]** The saved automations refer to ChatGPT conversation threads and have recent completion metadata. **[Confirmed — observed]** Readable results were recorded as ChatGPT messages. **[Unknown]** Whether each result reached the user's notification UI, email, push notifications, or another channel: recorded `delivery_status` is `unknown`. No external dashboard or digest delivery is established.

### Exact saved prompts, with explicit privacy redactions

The following reproduce the accessible prompt wording except for replacements shown in square brackets. Those replacements make this **redacted transcription**, not byte-for-byte reproduction. Company/role preferences that define the workflow are retained, while school identity and private profile details are generalized.

**A. Fresh New-Grad Role Scan — [Confirmed — instruction]**

> Find newly posted roles I could realistically apply to, prioritizing new-grad and early-career Software Engineer roles and using ML/AI Engineer or closely related roles as secondary targets. EXCLUDE all 100% remote / remote-only positions, even if otherwise strong fits. Recommend only positions with an explicit on-site or hybrid work arrangement; prioritize major U.S. cities, especially NYC and the Bay Area. If the arrangement is unclear, verify it before recommending; do not assume a remote listing offers an office option. Prefer roles posted within the last 24-72 hours, FAANG/big tech and strong smaller companies, and positions compatible with a December 2026 [CS master's] graduate. Cross-check against my job application tracker and recent application confirmations when available so you do not recommend roles I already applied to or was rejected from. For each strong match, give me the role, company, location, posting freshness, verified work arrangement, why it fits me, and application link. Rank only genuinely worthwhile opportunities rather than filling a quota. For strong roles, preview the application form when accessible and check for required short-answer questions. If required short-answer questions are visible, surface them and draft truthful responses grounded in my latest resume and actual experience; ask me a clarifying question when information needed for a good response is missing rather than inventing it. When a particularly high-value role would materially benefit from tailoring, tell me exactly which resume bullets/keywords should be changed and whether a cover letter is worth creating; do not fabricate experience or qualifications.

**B. Daily Networking Plan — [Confirmed — instruction]**

> Review my job-search and networking priorities and prepare today's highest-value outreach plan for new-grad SWE roles, with ML/AI-related roles as secondary targets. Aim for roughly 3 to 5 high-quality contacts when appropriate and include due follow-ups. For new outreach, prioritize [university] alumni first, especially alumni at companies with active or strong prospective applications; within that group favor recruiters/hiring managers and engineers closely aligned with the target team who could provide insight, introductions, referrals, or recruiter contact. Then consider non-[university] recruiters, hiring managers, and highly relevant engineers. Use both LinkedIn and professional email strategically. For each contact, choose the best channel: use LinkedIn connection requests/messages when that is the natural professional path, and use email when a legitimate publicly available professional address or an address from connected sources is available. Never guess or fabricate email addresses. With LinkedIn Premium available soon, make short personalized messages the default when messaging is possible, while preserving InMail for especially high-value people who cannot be reached through a normal connection/message. For email, prioritize recruiters and hiring managers, then highly relevant engineers/alumni. Draft concise personalized outreach for each recommended contact, but do not send anything without my approval. Avoid duplicate outreach by checking existing networking history when available. Focus on genuine conversations that can lead to referrals, introductions, recruiter contact, or interviews. Prefer FAANG/big tech while remaining open to strong smaller companies, especially on-site or hybrid roles near major U.S. cities.

**C. Recruiting Action Watch — [Confirmed — instruction]**

> Review my connected Gmail for recruiting and job-search action items that require something from me, including interview scheduling requests, confirmed interviews, confirmed coffee chats, assessments or coding challenges, recruiter-requested follow-ups, application tasks, forms, deadlines, and other time-sensitive recruiting actions. Cross-check later emails and the relevant thread for credible signals that each item was completed, submitted, scheduled, cancelled, withdrawn, rejected, superseded, or otherwise no longer requires action. If there is credible completion or closure evidence, do not remind me about that item. For unresolved items, notify me with the company/contact, required action, deadline or confirmed date/time, and the recommended next step. For a confirmed interview, coffee chat, recruiter call, or other recruiting event with an explicit date and time, check my connected Google Calendar and, when no matching event already exists, add it to my calendar using the email's confirmed date/time, timezone, meeting details, and relevant context. Never invent a time, deadline, meeting link, attendee, or event detail. Do not create calendar events for assessments or tasks that only have a deadline unless the email explicitly schedules a specific appointment/time. Avoid duplicate calendar events. If there are no unresolved recruiting action items, do not notify me.

## 4. Job discovery and recommendation logic

- **[Confirmed — instruction] Sources:** Locate current postings and provide application links, with preference for verifiable official details. Compare against a job application tracker and recent application confirmations **when available**. **[Unknown]** The actual discovery providers (employer sites, job boards, third-party APIs, search engine, curated feeds), query strategy, and extraction pipeline. Specialized inactive company-watch prompts requested official career pages, but do not establish the active general scanner's sources.
- **[Confirmed — instruction] Recency:** Prefer postings within **24–72 hours**. This is a preference, not a proven hard cutoff. **[Unknown]** How reposts, refreshed postings, timestamps without timezone, or stale listing dates are treated in actual runs.
- **[Confirmed — instruction] Fit:** New-grad/early-career SWE first; ML/AI secondary; graduation eligibility, relevant skills and actual experience, major-city location, on-site/hybrid arrangement, and high-quality employers. Rank meaningful matches rather than fill a quota. **[Unknown]** Numeric fit scoring, model weights, thresholds, or any supervised ranking labels.
- **[Confirmed — instruction] Hard exclusions:** Fully remote/remote-only; roles already applied to or rejected from **when history is available**; roles with unverified work arrangement should be verified **before** recommendation. Inactive employer-specific watches also requested explicit graduate-date checks and exclusion of prior requisitions, but are not evidence of a universal enforced rule.
- **[Confirmed — instruction] Deduplication:** Cross-check application tracker and confirmations to avoid already-applied/rejected positions. **[Unknown]** Whether **previously seen but unapplied** listings are remembered, whether deduplication spans runs or company requisition IDs, and how duplicate employer/agency listings are merged.
- **[Confirmed — instruction] Evidence:** For each recommended role, include posting freshness, verified work arrangement, relevant fit rationale, and an application link. **[Unknown]** Whether every historic result actually contains clickable primary-source links and exact verification timestamps.
- **[Inferred — conservative interpretation]** If a posting date cannot be verified, label freshness **unverified** rather than falsely claiming “posted today”; if the on-site/hybrid requirement cannot be verified, withhold the listing under the stated instruction. If graduate eligibility is ambiguous, flag it for manual review rather than declaring eligibility. **[Unknown]** Whether the existing scanner implements these fallbacks consistently; no readable latest job-scan output was available.
- **[Confirmed — instruction] Application-form preview:** Preview strong-role application forms when accessible, surface required short-answer questions and truthful draft answers, and recommend selective resume tailoring. **[Unknown]** Form-access success rate or whether browser restrictions prevent previewing particular forms.

## 5. Networking and hiring-manager/recruiter discovery

- **[Confirmed — instruction]** Propose about three to five high-quality contacts when appropriate, not mechanically; prioritize alumni at companies with active/prospective applications, then aligned recruiters, hiring managers, and engineers; consider non-alumni next. Draft a personalized LinkedIn message, InMail, or legitimate professional email. Never fabricate addresses; never send without approval; check prior outreach history when available.
- **[Confirmed — observed]** The November 19 plan identified warm connections, potential alumni introductions, and a recruiter follow-up, explained contact/channel priorities, and produced draft messages. It searched connected email for possible duplicate outreach. It also expressly warned that LinkedIn invitation/message state was not independently verified. The record says it **did not send** anything.
- **[Confirmed — observed via user reports]** The user has recorded invitations, connection acceptances, referral discussions and follow-ups in conversation; saved context uses pending/accepted labels. This is evidence of human-guided tracking, not proof of LinkedIn API synchronization.
- **[Unknown]** An automated, exhaustive recruiter/hiring-manager directory; verified reporting chains to a target job; consistent alumni matching; automatic LinkedIn read/write capability; direct recipient-email validation beyond available evidence; and conversion rates to referral/interview. “Hiring-manager discovery” is a **requested prioritization capability**, not a verified comprehensive implementation.

## 6. Application, interview, OA, deadline, and next-action tracking

- **[Confirmed — saved context]** The user has a named job-and-network tracker, has requested reconciliation with application confirmations, and has manually told the assistant about applications, completed online assessments, interviews and networking milestones. Its workbook schema, exact location, update history, and current correctness are **[Unknown]** because the workbook was not inspected.
- **[Confirmed — instruction]** The recruiting monitor reads connected Gmail, checks follow-up messages and full threads for completion/closure, and suppresses already-resolved tasks. It checks Google Calendar and is authorized by its saved prompt to add **confirmed, specifically timed** recruiting appointments if absent; it must not create deadline-only calendar events or invent details.
- **[Confirmed — observed]** In the November 19 result, a recruiting run identified four open items across an OA, an account activation, a confirmed interview, and a take-home exercise. It separately noted closed applications, found a confirmed meeting already present on Calendar, and created no new event.
- **[Confirmed — observed via user reports]** Completion reports for some past OAs and interviews have been used to request suppression of obsolete reminders. This demonstrates a manual correction channel, not guaranteed persistent structured state.
- **[Unknown]** Exact persistence mechanism: spreadsheet cells, ChatGPT memory/context, task histories, email as source of truth, or some combination; whether an automation writes back to the tracker; whether status changes are transactionally audited; and whether a previously completed item is always suppressed in all future runs.
- **[Inferred — design caution]** The system currently operates across several potentially inconsistent evidence surfaces: user statements, saved context, tracker, inbox, calendar and historical task output. A rebuilt project needs explicit source attribution, action status, timestamp and user override.

## 7. Model judgments versus tools and fixed rules

| Layer | Evidenced role | Status |
|---|---|---|
| Scheduling | Stored RRULEs cause periodic task invocations or condition-watch checks; runtime stores run metadata | **[Confirmed — configuration]** |
| External reads | Recorded runs say Gmail messages and Calendar were checked; networking run says sent mail was searched | **[Confirmed — observed at report level]**, not an independent audit of every call |
| Search/retrieval | General role search and profile matching are requested; exact search source and implementation unavailable | **[Confirmed — instruction] / [Unknown — execution]** |
| LLM interpretation | Judge role relevance and evidence quality, write explanations, prioritize outreach, infer action state from email threads, draft text | **[Inferred from prompt and resulting natural-language outputs]**; exact prompts/model versions unavailable |
| Fixed policy constraints | No fully remote listings; do not fabricate dates, credentials or addresses; suppress known completed actions; avoid duplicate calendar events; no outreach without approval | **[Confirmed — instructions]**; enforcement by code versus model instructions is **[Unknown]** |
| Writes/side effects | Task prompt permits conditional Calendar event creation; sending networking outreach requires approval | **[Confirmed — instruction]**; latest inspected runs report no outbound outreach, tracker writes, or Calendar additions |
| Human decisions | Select roles, approve messages, submit applications, resolve ambiguities and report completions | **[Confirmed — conversation history]** |

**[Unknown]** Whether there is any deterministic rule engine, database constraint, schema validator, scoring function, automatic browser application submission, or transaction log. A written prohibition in a prompt should not be represented as programmatically enforced.

## 8. Anonymized representative output

**[Confirmed — observed, anonymized paraphrase]** The following captures the **structure and kinds of conclusions** of an accessible November 19 recruiting-monitor result. Names, employers, links, exact meeting identifiers, and private correspondence are intentionally removed. This is **not** a fabricated claim that a job-scan output was observed.

| Priority | Organization | Finding | Proposed next action | Timing confidence |
|---|---|---|---|---|
| 1 | Employer A | Coding assessment still unresolved; no later submission confirmation found | Complete the assessment | Estimated deadline window; exact expiration unverified |
| 2 | Employer B | Careers-account activation request | Activate account | No deadline stated |
| 3 | Employer C | Recruiting interview confirmed and already on Calendar | Prepare and attend; no duplicate event | Exact appointment time confirmed in underlying source |
| 4 | Startup D | Take-home exercise requested | Prepare and submit response if proceeding | No deadline stated |

**[Confirmed — observed]** The original run separately marked some applications closed and said no Calendar events were added. The task delivery status was not confirmed. **[Unknown]** Whether any of these actions was subsequently completed.

**[Illustrative — proposed MVP output, not observed]** A job-shortlist row might be: `Company A | New Grad Backend Engineer | NYC | hybrid verified [source URL] | posted date unverified | degree window needs review | strong Python/SQL/API fit | status: new`. This shows a proposed representation, **not** a verified real vacancy.

## 9. What works, failures and manual effort

### Supported strengths

- **[Confirmed — observed]** An active scheduler stores detailed prompts and creates recorded run results. Two Nov 19 results were readable and completed.
- **[Confirmed — observed]** Networking output combined warm contacts, relevant employer context, outreach drafts, duplicate-email checks, and an explicit warning about unverified LinkedIn state.
- **[Confirmed — observed]** Recruiting output synthesized multiple inbox items, separated required actions from ordinary opportunities, recognized later closure evidence, and avoided a duplicate calendar addition.
- **[Confirmed — instruction]** Job matching is constrained by actual graduation, work arrangement, candidate fit and nonduplication rather than indiscriminate job-volume maximization. Its real-world precision is **[Unknown]** without the latest run output or an evaluation dataset.

### Known limits and friction

- **[Confirmed — observed]** The read-only attempt to fetch the latest role-scan result failed. This is a visibility/evidence limitation of **this review**, not proof the scheduled scan itself failed.
- **[Confirmed — observed]** LinkedIn invitation/message state could not be independently verified by a networking run. Users must check invitation status before acting.
- **[Confirmed — observed / saved context]** The user frequently reports completed assessments, applications, invitations and interviews and requests deduplication/reconciliation. Manual status correction remains material.
- **[Confirmed — saved context]** Some roles have unclear graduation eligibility, shifting work arrangements, and application-specific questions; the user has requested explicit eligibility checks, verified location/work style, and truthful short-answer support.
- **[Confirmed — instruction]** Avoiding repeated completed/rejected roles is an important design objective. **[Unknown]** How often existing runs have actually failed at deduplication; no measured false-positive count is available.
- **[Confirmed — observed]** The Nov 19 networking result reported no tracker modifications; the Nov 19 recruiting result reported no Calendar addition. These show review-oriented operation, not fully automated state synchronization.
- **[Unknown]** Recall/precision, hallucination rate, source freshness, posting-date verification rate, broken-link rate, duplicate rate, cost/latency, email false-positive/negative rate, and long-term operational reliability.

### Features specifically requested or revised

- **[Confirmed — conversation and prompts]** Enforce no remote-only recommendations, prioritize on-site/hybrid in preferred locations, and verify ambiguity rather than assuming an office option.
- **[Confirmed — conversation and prompts]** Preview required application essays and draft answers, with no fabricated experience; suggest selective resume changes for strong opportunities.
- **[Confirmed — conversation and prompts]** Deduplicate against applied/rejected jobs, known recruiting closures and previously contacted people.
- **[Confirmed — conversation and prompts]** Surface hiring managers/recruiters and school alumni; prefer high-value networking and professional channels; send nothing without approval.
- **[Confirmed — conversation and prompts]** Monitor email for interview/OA actions, suppress already-completed actions, and put only confirmed timed meetings on Calendar without duplicates.
- **[Confirmed — conversation history]** The user previously requested a separate interactive interview-preparation workspace, including stages, STAR stories, practice and confidence/status tags. This is related but not required for the minimal job-discovery product.

## 10. Smallest useful local MVP for students and recent graduates

The **recommended MVP is a local job-discovery and shortlist application**, not a full clone of all scheduled assistants. It should work without LinkedIn automation, email authorization, calendar writes or real applicant tracking systems.

### Essential scope (recommended; not claimed to exist)

1. **Student profile:** one editable JSON/SQLite profile containing degree and expected graduation month, work authorization constraints, technical skills, role families, location and work-style preferences, and user-entered projects. Optional resume import; users confirm extracted facts before use. Keep resume-version IDs and a clear canonical profile.
2. **Ingestion:** start with a small set of public employer-careers pages or a permitted job feed, plus a user-pasted posting URL. Store raw title/company/location/description, source URL, fetch time, published date when present, and extraction confidence. Respect terms and avoid anti-bot circumvention.
3. **Eligibility filter:** deterministic rules for explicitly remote-only listings, preferred geography and known graduation/experience requirements. Treat missing or contradictory facts as `unknown / review`, not positive matches. Avoid assuming US work authorization automatically implies eligibility for all roles.
4. **Deduplication:** canonical job key (`source + requisition_id`, fallback normalized company/title/location/URL); persist seen-at and last-seen timestamps, user statuses (`new`, `saved`, `applied`, `rejected`, `hidden`), and history across refreshes. Distinguish **seen** from **applied**.
5. **Fit explanation:** simple auditable weights or rules (role category, skills evidence, graduation fit, location/work style). Optionally use an LLM only to explain evidence and highlight ambiguity, not to fabricate eligibility. Show specific supporting posting snippets and missing requirements.
6. **Local review UI:** recent candidate listings; source and verification link; labels `verified`, `unverified`, `conflict`; explicit reasons for exclusion; save/hide/apply-status controls; last checked time. Provide a small shortlist with no pressure to fill a fixed number.
7. **Refresh and evaluation:** manual “scan now” first; optional local scheduled refresh after the base workflow works. Maintain a fixture set of postings testing remote-only, ambiguous hybrid, expired/reposted, mismatched graduation, duplicate URL and previously-applied cases. Report precision of hard filters and duplicate suppression.

**[Inferred — feasibility]** A practical stack is Python ingestion, SQLite, a basic local web UI (e.g., Streamlit or FastAPI plus a lightweight frontend), and a small number of source adapters. This is a design suggestion, **not** evidence about the existing architecture. A source-only demonstration with 20–50 test listings and transparent labels is sufficient for a meaningful course milestone.

### Explicitly optional, out of MVP

- **Networking and recruiter/hiring-manager discovery:** contact research, alumni relevance, approval-gated outreach drafts, and manual outreach-status logging; never auto-send without express permission.
- **Essay/resume assistance:** application short-answer extraction where accessible, evidence-based drafts, and clearly marked resume tailoring suggestions. Require user review and keep a version history.
- **Interview/OA/action tracking:** opt-in Gmail/Calendar integration, completion and closure detection, deadlines, calendar deduplication and explicit audit logs. Begin with manual task entry; consider read-only inbox parsing before any calendar writes.
- **Advanced operations:** scheduled notifications, multi-resume comparison, cross-account synchronization, privacy/retention controls, and automatic source validation. These are later extensions, not demonstrated MVP requirements.

### Local data model sketch (recommended, not existing)

`candidate_profile`, `resume_versions`, `job_sources`, `jobs`, `job_evidence`, `job_status_events`, and `scan_runs`. Optional future tables: `contacts`, `outreach_events`, `applications`, `recruiting_actions`, `calendar_event_links`. Every automated observation should preserve its source URL or message reference (where authorized), observed time, confidence, and any user override.

## Concise unknowns and information to provide

1. **Actual job-scan outputs:** 2–3 full, redacted historical runs, including links and failure examples, to verify freshness, sources and filtering.
2. **Tracker schema:** sanitized sheet/database column names, sample rows and who/what edits them. Clarify whether it is authoritative or merely one evidence source.
3. **Resume handling:** which resume is canonical, where versions reside, and how conflicting education dates/skills are reconciled.
4. **Job-source inventory:** exact boards, employer pages, APIs or search tools currently used; any source restrictions and repost handling.
5. **Persistence and deduplication:** how already-seen jobs, applications, rejections and outreach are carried between runs; job identity key; retention policy.
6. **Execution and delivery:** actual run-level tool logs, notification surfaces, failure/retry behavior, and whether any Calendar event was successfully created by the monitor in the past.
7. **Quality evidence:** examples of false positives, missed eligible roles, stale listings, duplicate recommendations, unverified dates and mistaken action reminders.
8. **MVP choices:** local OS, programming stack/course constraints, permitted source or sample-data approach, evaluation targets, and whether manual URL input is acceptable before automation.

**Bottom line — [Inferred recommendation]:** Preserve the distinctive user value—personal eligibility filters, trustworthy posting evidence, persistent deduplication, and a small defensible shortlist—before adding networking or inbox automation. The accessible material establishes a capable *set of instructions* and two relevant recorded results, but does **not** establish a comprehensive implemented architecture or verified reliability.
