# Project vision

Status: updated on November 24, 2026 with the confirmed product name, model, sources, refresh behavior, and resume-bullet scope. 

## Product and users

- Product name: AI Job Application Agent
- One-sentence description: A local application that helps students and recent graduates review a personal profile, receive scheduled and explained recommendations for jobs and internships, and review a suggested arrangement of their existing resume bullets for a selected role. It does not submit applications.
- Primary users and their context: Students and recent graduates looking for internships and entry-level jobs. They may keep several resumes that emphasize different projects. Mid-level and senior job seekers are a later audience.
- Problem and current workaround: These candidates search across job boards, read long descriptions, and decide which roles fit their skills, experience, and preferences. Broad results and generic recommendations send them to roles that fit poorly. Finding newly posted roles means repeating that screening. Today they do this by hand.
- Why solving this problem matters: A smaller set of recent, explained matches lets a candidate spend time on applications instead of rereading listings that do not fit.
- Why an LLM is appropriate instead of ordinary search/filtering alone: Job descriptions and resumes use different wording for the same skill or project. Keyword filters miss those links and cannot explain a gap. The LLM compares the language in a listing with the skills, projects, and experience in a user-reviewed profile, explains the connection, and points out missing or unclear requirements. Posting dates, eligibility, and other facts still come from the retrieved source. The model does not supply a fact the source does not contain.

## Core user journey

1. User starts with: Several resumes and a need to find internships or entry-level jobs posted recently, without reading every board from scratch.
2. User provides: Uploaded resume files, pasted profile text, manual preferences such as target roles, locations, work style, and eligibility notes, and any full job text the user pastes, including a LinkedIn job.
3. Product retrieves or processes: The application extracts skills, projects, and experience, keeps the source of each claim, and shows that profile for correction. While the app is running it retrieves listings from Adzuna and USAJOBS on the schedule below, stores the source URL, fetch time, and posting date when the source provides one, and suppresses duplicates. Pasted jobs are stored the same way.
4. LLM interprets or decides: OpenAI `gpt-6.1-terra` extracts profile claims and, after retrieval tools return listing details, decides which roles are worth explaining. It writes an explanation tied to the confirmed profile and the listing text it actually received, including gaps and unclear requirements. For a selected job it proposes which existing bullets to emphasize or reorder. It does not invent a posting date, an eligibility fact, a qualification, or a new resume bullet.
5. User reviews and acts on: The user corrects the profile, reads each explanation and source link, saves or hides a listing, accepts or rejects the bullet suggestion for a selected job, and reads results in the app. If the user turns email on, results from a scan that finishes while the app is running can also be emailed.

Concrete scenario: A recent graduate uploads two resumes and pastes a short profile. The app proposes extracted claims, including a Python and SQL project, and shows which resume each claim came from. The graduate corrects one claim, adds a preference for entry-level software roles in a chosen city, and pastes one LinkedIn job description. At the next scan, the app shows internships and entry-level jobs with postings from the last 72 hours first, each with a source link and a short explanation of fit and gaps. The graduate saves two roles and accepts a reordered set of existing bullets for one of them. A later scan does not present those saved roles again as new.

## MVP features in scope

The MVP is one profile-to-shortlist workflow that can be demonstrated on a laptop by December 16, 2026.

| ID | Feature | User value | Observable acceptance criterion |
|---|---|---|---|
| MVP-01 | Profile from resumes, pasted text, and manual preferences, with user review | The user controls one profile built from every resume and can correct it before matching uses it | Given two resumes, pasted profile text, and one manual preference, the app lists extracted skills, projects, and experience and shows the source of each claim. A rejected claim is not used in later matching. A corrected claim is the value used afterward. |
| MVP-02 | Scheduled discovery that puts postings from the last 72 hours first | The user sees recent roles without repeating a full manual search | While the app is running, a scan starts every 4 hours and when the user chooses Scan now. Each listing stores its source URL, fetch time, and posting date when the source provides one. Listings whose posting date is inside the last 72 hours are ordered before older listings. A missing posting date is labeled unknown and is not described as posted within 72 hours. While the app is closed, no scan runs and no email is sent. On the next launch the last saved results appear, and one catch-up scan runs if the last successful scan is more than 4 hours old. |
| MVP-03 | Grounded fit explanations | The user can see why a role may fit and what is missing or unclear | Each recommended listing includes a source link and an explanation that names at least one confirmed profile claim and one phrase or requirement from the listing. Gaps are stated as gaps. The explanation adds no skill, date, eligibility fact, or employer detail that is absent from both the profile and the listing. |
| MVP-04 | Save, hide, and duplicate suppression | The user keeps a shortlist and is not shown the same listing again as new | The user can save or hide a listing. A later scan does not present a saved or hidden listing as a new recommendation. Two listings that share a source and requisition id, or the same normalized company, title, location, and URL, appear once. |
| MVP-05 | In-app results by default, with optional email | The user reads results in the app and can opt into email | With the default setting, results appear in the app and no email is sent. When the user enables email and enters an address, a scan that finishes while the app is running can send that same result set to the address. A closed app does not send email. |
| MVP-06 | User-reviewed arrangement of existing resume bullets for one selected job | The user sees which confirmed bullets to emphasize for a role they are considering | For a selected listing, the app proposes an order and subset of bullets that already exist in the confirmed profile, and each bullet shows its source claim. The proposal adds no employer, skill, date, or metric that is absent from the confirmed profile. Nothing is saved until the user accepts it. Rejecting the proposal leaves the profile unchanged. |

## Features explicitly out of scope

| Feature | Reason for excluding it from the MVP |
|---|---|
| Networking opportunity discovery | Recorded as a stretch goal. The committed journey is job and internship discovery. |
| Hiring-manager and recruiter discovery | Recorded as a stretch goal. It needs people search and contact data this MVP does not collect. |
| Application-essay preview and sample answers | Recorded as a stretch goal. The README places essay assistance outside the committed MVP. |
| Automated resume rewriting | Inventing employers, skills, dates, metrics, or new bullets stays out of the MVP. Selecting and reordering bullets that are already in the confirmed profile is MVP-06 and requires the user's acceptance. |
| Interview, online-assessment, and deadline tracking | Present in the reference system only. It needs mailbox or calendar access that this MVP does not use. |
| Automatic job applications | The user decides where to apply and submits applications outside this product. |
| Automatic outreach or sending messages to people | Outreach is outside the committed MVP, and the product does not send messages on the user's behalf. |
| Direct LinkedIn account connection, profile fetch, or automated LinkedIn job search | Profile text is pasted by the user. A LinkedIn job enters the product only when the user pastes the job text, or pastes the job URL together with the job text. The product does not sign in to LinkedIn or download LinkedIn jobs on its own. |
| Accounts for multiple users | One local user is enough to demonstrate the journey on a laptop. |
| Unrestricted scraping or bypassing site controls | Live search is limited to the Adzuna and USAJOBS APIs under their terms. LinkedIn and any other board are included only through text the user pastes. |
| Cloud hosting | The assignment accepts a product that runs on the team's laptops. |

## LLM and data boundaries

- Planned provider and model: OpenAI hosted API, model id `gpt-6.1-terra`. Tool calls use the Responses API. Profile extraction may set reasoning effort to `none`. The standard rates published on November 24, 2026 are $1 per million input tokens and $5 per million output tokens. If the team cannot use an OpenAI key, the fallback model is Anthropic `claude-haiku-5-5`. `gpt-6.2-astra` is a higher-cost option and is not the planned model. The API key stays in local configuration and is not committed.
- LLM-dependent features: Extraction of skills, projects, and experience from resumes and pasted profile text. Comparison of a confirmed profile with a retrieved or pasted listing. A written explanation of fit, gaps, and unclear requirements. Choosing which retrieved listings are worth explaining after tools return listing details. For one selected job, a proposed order and subset of existing confirmed resume bullets.
- Agent decisions and available tools, if any: The agent may call tools that search the Adzuna US jobs API and the USAJOBS API, and a tool that reads a job the user pasted. It inspects the returned text before it writes a recommendation or a bullet arrangement. Scheduling, storage, duplicate detection, and email or in-app delivery are application code. The model does not call LinkedIn.
- Supported opportunity sources and access method: Five sources. (1) Adzuna US search API at `https://api.adzuna.com/v1/api/jobs/us/search/{page}`, with a local `app_id` and `app_key`, for title, company, location, redirect URL, and posting date. Adzuna returns a description snippet, so an explanation may use only that snippet unless the user pastes the full text. Displayed Adzuna listings are labeled Adzuna and link to Adzuna. A salary marked as predicted is labeled an estimate or omitted. (2) USAJOBS API for US federal jobs, with a local API key, using the fuller description when the API returns one. (3) A LinkedIn job only when the user pastes the job text, or pastes the job URL together with the job text. (4) Any other full job text the user pastes. (5) A fixture set of listings stored in the repository for a demo when a live API fails. Each stored listing keeps title, company, location, the description text actually received, source URL, fetch time, and posting date when present.
- Source links/evidence shown to users: Every recommendation shows a source link. The explanation points at a specific part of the listing and a specific confirmed profile claim. Posting date and eligibility are shown only when the source provides them.
- Treatment of missing information and uncertain matches: Missing posting date, work arrangement, eligibility, or a required skill is labeled unknown or shown as a gap. The product does not treat unknown as a match. The model does not fill a quota of recommendations.
- Behavior when retrieval or model calls fail: If a source fails, the app shows the error and keeps the last successful results, and the demo can run on the saved listing set. If the model fails, the app does not invent an explanation. Listings can still appear with their source data and an explicit statement that the explanation is unavailable.
- Personal data collected, retained, or sent to a provider: The local app stores uploaded resumes, pasted profile text, pasted job text, manual preferences, the confirmed profile, saved listing status, and scan results. Text sent to the model is limited to the profile content needed for extraction or explanation and the listing text being judged. API keys and private resume files stay out of git. The user can delete the local profile data.
- Actions requiring user review: Extracted claims are not used for matching until the user confirms or corrects them. A suggested bullet arrangement is not saved until the user accepts it. The user chooses what to save. The product does not submit applications or send outreach. Email of results is off until the user enables it, and a closed app does not send email.

## Success criteria and feasibility

These are the demo bars for the fixed sample profiles and listings. The team can tighten them before implementation. They are pass/fail checks on that fixture set, not a claimed production accuracy rate.

| Goal | Measurement or test scenario | Target |
|---|---|---|
| Useful results | Run the fixture set that includes a fresh posting, an older posting, a missing date, a duplicate, an already saved listing, an unclear requirement, and a strong skill overlap. | Every recommended fixture is ordered by the 72-hour rule, duplicates and already saved listings are not shown as new, and the shortlist is not padded to a fixed count. |
| Factual grounding | Review each fixture explanation against the source listing and the confirmed profile. | Each explanation cites one profile claim and one listing detail. Dates, eligibility, and qualifications that the source does not state are labeled unknown or omitted. The review finds no invented fact. |
| Complete user journey | On a team laptop, load the sample resumes and preferences, paste one job description, run a scan on the fixture set, and if a live key is configured, run one Adzuna or USAJOBS retrieval. | The reviewer can correct the profile, read explanations and source links, save a shortlist, accept or reject a bullet arrangement made only from confirmed bullets, see a duplicate suppressed, and see an explicit error when the model or a source is turned off. Closing the app sends no email. |

- Team capacity and key dependencies: Four members, Yiyang Cheng (yc3259), Alyssa Cohen (ac2726), Don Seo (ds2549), and Dennis Chen (dc777), meet twice a week through December 16, 2026. No application code exists yet. The build depends on a local OpenAI API key for `gpt-6.1-terra`, or an Anthropic key for the fallback model, plus optional Adzuna and USAJOBS keys. The fixture set and pasted jobs do not depend on those job APIs.
- Major scope risks and fallback plan: Adzuna descriptions are snippets, LinkedIn cannot be searched automatically, model cost, resume extraction quality, and email delivery are the main risks. If a live source or the model is unavailable for the demo, the team runs the same journey on the fixture set and pasted text and shows the error states. In-app delivery is the path that must work. Email is demonstrated only while the app is running.
- Inception milestone: November 24, 2026, 11:59 PM Eastern (America/New_York).
- Final project deadline: December 16, 2026.
- Demo environment: The product runs locally on the team's laptops. Cloud hosting is not required.

## Open questions

These items were confirmed on November 24, 2026. No product decision in this document remains unresolved.

| ID | Unresolved decision | Owner | Resolve by | Related requirements question |
|---|---|---|---|---|
| OPEN-01 | Resolved. The product name is AI Job Application Agent. The product does not submit applications. | Whole team | 2026-11-24 | requirement-verification-questions.md Question 1 |
| OPEN-02 | Resolved. Planned model is OpenAI `gpt-6.1-terra` on the hosted API. Fallback is Anthropic `claude-haiku-5-5`. | Whole team | 2026-11-24 | readme-model-selection-questions.md Question 1 |
| OPEN-03 | Resolved. Sources are the Adzuna US API, the USAJOBS API, user-pasted LinkedIn job text, other user-pasted job text, and repository fixtures. | Whole team | 2026-11-24 | requirement-verification-questions.md Question 3 |
| OPEN-04 | Resolved. Scan every 4 hours while the app is running, plus Scan now. A closed app does not scan or send email. The next launch shows the last results and runs one catch-up scan if the last success is more than 4 hours old. | Whole team | 2026-11-24 | Delivery channel was already decided: in-app by default, email optional. |
| OPEN-05 | Resolved. A user-reviewed arrangement of existing resume bullets for one selected job is in the MVP. Inventing new resume content stays out. | Whole team | 2026-11-24 | README part 1 follow-up Question 2 |

## Team review

- All placeholders replaced with specific content.
- Scope, LLM rationale, sources, and success criteria agreed.
- Consistent with README and technical environment.
- Reviewed by the whole team.
