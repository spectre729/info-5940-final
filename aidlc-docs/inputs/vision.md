# Project vision

Status: Draft from the README and the recorded answers. Not team-approved. Open items are listed under Open questions and are not treated as decisions.

## Product and users

- Product name: No formal name is chosen. This document calls the product a local job and internship discovery assistant. The formal name is OPEN-01.
- One-sentence description: A local application that helps students and recent graduates review a personal profile and receive scheduled, explained recommendations for jobs and internships, with postings from the last 72 hours ordered first.
- Primary users and their context: Students and recent graduates looking for internships and entry-level jobs. They may keep several resumes that emphasize different projects. Mid-level and senior job seekers are a later audience.
- Problem and current workaround: These candidates search across job boards, read long descriptions, and decide which roles fit their skills, experience, and preferences. Broad results and generic recommendations send them to roles that fit poorly. Finding newly posted roles means repeating that screening. Today they do this by hand.
- Why solving this problem matters: A smaller set of recent, explained matches lets a candidate spend time on applications instead of rereading listings that do not fit.
- Why an LLM is appropriate instead of ordinary search/filtering alone: Job descriptions and resumes use different wording for the same skill or project. Keyword filters miss those links and cannot explain a gap. The LLM compares the language in a listing with the skills, projects, and experience in a user-reviewed profile, explains the connection, and points out missing or unclear requirements. Posting dates, eligibility, and other facts still come from the retrieved source. The model does not supply a fact the source does not contain.

## Core user journey

1. User starts with: Several resumes and a need to find internships or entry-level jobs posted recently, without reading every board from scratch.
2. User provides: Uploaded resume files, pasted profile text, and manual preferences such as target roles, locations, work style, and eligibility notes the user wants considered.
3. Product retrieves or processes: The application extracts skills, projects, and experience, keeps the source of each claim, and shows that profile for correction. On a schedule, it retrieves listings from the supported sources, stores the source URL, fetch time, and posting date when the source provides one, and suppresses duplicates.
4. LLM interprets or decides: The model extracts profile claims and, after retrieval tools search the supported sources and inspect a listing, decides which roles are worth explaining. It writes an explanation tied to the user's confirmed profile and the listing, including gaps and unclear requirements. It does not invent a posting date, an eligibility fact, or a qualification.
5. User reviews and acts on: The user corrects the profile, reads each explanation and source link, saves or hides a listing, and reads results in the app. If the user turns email on, the same results can also be emailed.

Concrete scenario: A recent graduate uploads two resumes and pastes a short profile. The app proposes extracted claims, including a Python and SQL project, and shows which resume each claim came from. The graduate corrects one claim and adds a preference for entry-level software roles in a chosen city. At the next scan, the app shows internships and entry-level jobs with postings from the last 72 hours first, each with a source link and a short explanation of fit and gaps. The graduate saves two roles. A later scan does not present those saved roles again as new.

## MVP features in scope

The MVP is one profile-to-shortlist workflow that can be demonstrated on a laptop by December 16, 2026.

| ID | Feature | User value | Observable acceptance criterion |
|---|---|---|---|
| MVP-01 | Profile from resumes, pasted text, and manual preferences, with user review | The user controls one profile built from every resume and can correct it before matching uses it | Given two resumes, pasted profile text, and one manual preference, the app lists extracted skills, projects, and experience and shows the source of each claim. A rejected claim is not used in later matching. A corrected claim is the value used afterward. |
| MVP-02 | Scheduled discovery that puts postings from the last 72 hours first | The user sees recent roles without repeating a full manual search | A scan stores each listing with its source URL, fetch time, and posting date when the source provides one. Listings whose posting date is inside the last 72 hours are ordered before older listings. A missing posting date is labeled unknown and is not described as posted within 72 hours. |
| MVP-03 | Grounded fit explanations | The user can see why a role may fit and what is missing or unclear | Each recommended listing includes a source link and an explanation that names at least one confirmed profile claim and one phrase or requirement from the listing. Gaps are stated as gaps. The explanation adds no skill, date, eligibility fact, or employer detail that is absent from both the profile and the listing. |
| MVP-04 | Save, hide, and duplicate suppression | The user keeps a shortlist and is not shown the same listing again as new | The user can save or hide a listing. A later scan does not present a saved or hidden listing as a new recommendation. Two listings that share a source and requisition id, or the same normalized company, title, location, and URL, appear once. |
| MVP-05 | In-app results by default, with optional email | The user reads results in the app and can opt into email | With the default setting, results appear in the app and no email is sent. When the user enables email and enters an address, the same result set can be sent to that address. |

## Features explicitly out of scope

| Feature | Reason for excluding it from the MVP |
|---|---|
| Networking opportunity discovery | Recorded as a stretch goal. The committed journey is job and internship discovery. |
| Hiring-manager and recruiter discovery | Recorded as a stretch goal. It needs people search and contact data this MVP does not collect. |
| Application-essay preview and sample answers | Recorded as a stretch goal. The README places essay assistance outside the committed MVP. |
| Automated resume rewriting | The README places it outside the MVP. Whether the user may review a recombination of existing bullets for one selected job is OPEN-05, not an approval to rewrite a resume automatically. |
| Interview, online-assessment, and deadline tracking | Present in the reference system only. It needs mailbox or calendar access that this MVP does not use. |
| Automatic job applications | The user decides where to apply and submits applications outside this product. |
| Automatic outreach or sending messages to people | Outreach is outside the committed MVP, and the product does not send messages on the user's behalf. |
| Direct LinkedIn connection, or fetching a profile from a LinkedIn URL | The recorded answer for the MVP is upload of resumes and paste of profile text. |
| Accounts for multiple users | One local user is enough to demonstrate the journey on a laptop. |
| Unrestricted scraping or bypassing site controls | Retrieval is limited to a small set of sources the team can access within those sources' terms. The specific sources are OPEN-03. |
| Cloud hosting | The assignment accepts a product that runs on the team's laptops. |

## LLM and data boundaries

- Planned provider and model: Not selected. The team will choose a hosted API or a local model, such as one served by Ollama, based on access, cost or hardware, and a trial of profile extraction and explanation quality. The choice is OPEN-02 and must be named in the README and the technical environment document before those documents are treated as final.
- LLM-dependent features: Extraction of skills, projects, and experience from resumes and pasted profile text. Comparison of a confirmed profile with a retrieved listing. A written explanation of fit, gaps, and unclear requirements. Choosing which retrieved listings are worth explaining after tools return listing details.
- Agent decisions and available tools, if any: The agent may call a small set of retrieval tools to search the supported sources and inspect a listing before it writes a recommendation. Scheduling, storage, duplicate detection, and email or in-app delivery are application code, not model decisions. Exact tool inputs and outputs are defined in application design, after OPEN-03.
- Supported opportunity sources and access method: A small set, not chosen yet (OPEN-03). Each adapter must store the raw title, company, location, description, source URL, fetch time, and posting date when present. A saved demo set of listings must support a repeatable demo when a live source is unavailable. The user can also paste a listing.
- Source links/evidence shown to users: Every recommendation shows a source link. The explanation points at a specific part of the listing and a specific confirmed profile claim. Posting date and eligibility are shown only when the source provides them.
- Treatment of missing information and uncertain matches: Missing posting date, work arrangement, eligibility, or a required skill is labeled unknown or shown as a gap. The product does not treat unknown as a match. The model does not fill a quota of recommendations.
- Behavior when retrieval or model calls fail: If a source fails, the app shows the error and keeps the last successful results, and the demo can run on the saved listing set. If the model fails, the app does not invent an explanation. Listings can still appear with their source data and an explicit statement that the explanation is unavailable.
- Personal data collected, retained, or sent to a provider: The local app stores uploaded resumes, pasted profile text, manual preferences, the confirmed profile, saved listing status, and scan results. Text sent to the model is limited to the profile content needed for extraction or explanation and the listing text being judged. API keys and private resume files stay out of git. The user can delete the local profile data.
- Actions requiring user review: Extracted claims are not used for matching until the user confirms or corrects them. The user chooses what to save. The product does not submit applications or send outreach. Email of results is off until the user enables it.

## Success criteria and feasibility

These are the demo bars for the fixed sample profiles and listings. The team can tighten them before implementation. They are pass/fail checks on that fixture set, not a claimed production accuracy rate.

| Goal | Measurement or test scenario | Target |
|---|---|---|
| Useful results | Run the fixture set that includes a fresh posting, an older posting, a missing date, a duplicate, an already saved listing, an unclear requirement, and a strong skill overlap. | Every recommended fixture is ordered by the 72-hour rule, duplicates and already saved listings are not shown as new, and the shortlist is not padded to a fixed count. |
| Factual grounding | Review each fixture explanation against the source listing and the confirmed profile. | Each explanation cites one profile claim and one listing detail. Dates, eligibility, and qualifications that the source does not state are labeled unknown or omitted. The review finds no invented fact. |
| Complete user journey | On a team laptop, load the sample resumes and preferences, run a scan on the fixture set, and if a live source is configured, run one live retrieval. | The reviewer can correct the profile, read explanations and source links, save a shortlist, see a duplicate suppressed, and see an explicit error when the model or a source is turned off. |

- Team capacity and key dependencies: Four members, Yiyang Cheng (yc3259), Alyssa Cohen (ac2726), Don Seo (ds2549), and Dennis Chen (dc777), meet twice a week through December 16, 2026. No application code exists yet. The build depends on a named model the team can call from a laptop and on either a small permitted source or the saved demo listings.
- Major scope risks and fallback plan: Source access, model quality and cost, resume extraction quality, and reliable scheduling or email are the main risks. If a live source or the chosen model is unavailable for the demo, the team demonstrates the same journey on the fixture set and shows the error states. Email can be shown as a user setting with a recorded test send, while in-app delivery remains the path that must work.
- Inception milestone: November 24, 2026, 11:59 PM Eastern (America/New_York).
- Final project deadline: December 16, 2026.
- Demo environment: The product runs locally on the team's laptops. Cloud hosting is not required.

## Open questions

These items are unresolved. They are also tracked in the requirements question files named below. This draft does not answer them.

| ID | Unresolved decision | Owner | Resolve by | Related requirements question |
|---|---|---|---|---|
| OPEN-01 | Formal product name | Whole team | Before requirements approval | None. Product direction is requirement-verification-questions.md Question 1. |
| OPEN-02 | Provider and exact model, including who has access and the cost or hardware limit | Part 3, then the whole team | Before the README and technical environment document are finalized | readme-model-selection-questions.md Question 1 |
| OPEN-03 | Which listing sources are supported, how they are accessed, and what the saved demo set contains | Part 3, then the whole team | Before requirements approval | requirement-verification-questions.md Question 3 |
| OPEN-04 | Refresh frequency, and what happens while the local app is closed | Part 3, then the whole team | Before requirements approval | None. Delivery channel is already decided: in-app by default, email optional. A four-hour reference schedule was not adopted. |
| OPEN-05 | Whether a user-reviewed recombination of existing resume bullets for one selected job is inside the MVP. Automated rewriting stays out unless the whole team changes that decision. | Part 2 and Part 4, then the whole team | Before requirements approval | README part 1 follow-up Question 2 asked for one reviewed profile. The later sentence about mixing bullets is not yet reconciled with the README exclusion. |

## Team review

- [ ] All placeholders replaced with specific content.
- [ ] Scope, LLM rationale, sources, and success criteria agreed.
- [ ] Consistent with README and technical environment.
- [ ] Reviewed by the whole team.
- Reviewers and review date: Pending. No team review of this draft is recorded.
- Approval reference in audit.md: None. This draft is not an approval.
