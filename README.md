# info-5940-final

## Team name and netID

- Yiyang Cheng yc3259
- Alyssa Cohen ac2726
- Don Seo ds2549
- Dennis Chen dc777
## Coding Agent and AI-DLC version


- Coding Agent: Codex

- AI-DLC version: 1.0.1

## Problem and rationale for using LLMs

Students and recent graduates looking for jobs and internships often have to search across job boards, read lengthy descriptions, and decide whether each opportunity fits their background. Broad search results and recommendations can leave candidates spending time on roles that do not match their skills, experience level, or preferences. Repeating this process to find newly posted opportunities adds to the effort. Our project aims to reduce that manual screening by providing scheduled, personalized recommendations that prioritize jobs and internships posted within the last 72 hours.

An LLM is useful for comparing the varied language in job descriptions with the skills, projects, and experiences described in a candidate's resumes and profile. Candidates may maintain several resumes that emphasize different parts of their background, so the product will bring that information, pasted profile text, and manual additions into a user-reviewed profile. The LLM can use this context to identify relevant connections and explain why a role may be worth considering, including gaps or uncertain requirements. Recommendations should link to source listings, with posting dates and eligibility details grounded in those sources rather than assumed by the model. The goal is to help candidates make informed application decisions and spend less time repeatedly screening listings. Networking, recruiter discovery, and application essay assistance are stretch goals beyond the core discovery workflow.

## Planned LLM integration

The planned workflow uses an LLM to extract skills, projects, and experience from uploaded resumes and pasted profile text, then combine them with manually entered preferences into a profile the user can review and correct. During job discovery, the LLM will compare retrieved listings with this profile, prioritize potentially relevant opportunities, and generate explanations grounded in the candidate's experience and the listing. It should highlight missing qualifications or unclear requirements rather than inventing a match. The proposed agentic component will use a limited set of retrieval tools to search supported sources and inspect listing details before producing recommendations; the supported live sources are Adzuna US and USAJOBS, supplemented by user-pasted job descriptions and demo fixtures. LinkedIn input is pasted text, with no account connection or automated LinkedIn search.

Scheduling, saved results, duplicate detection, and notification delivery will be handled by application code. Users will receive results in the app by default, with email delivery available as an option. Posting dates and other factual details must come from retrieved sources, with unavailable information marked as unknown. The reviewed vision names OpenAI's hosted API with planned model `gpt-6.1-terra`. It records Anthropic `claude-haiku-5-5` as a deliberately configured fallback. Actual model access, cost, and extraction/matching quality will be validated before implementation depends on that choice.

## Project scope and feasibility

By the December 16 final-project deadline, our target is a locally running application for students and recent graduates that accepts multiple resumes, pasted profile text, and manual preferences; builds a user-reviewed candidate profile; and periodically retrieves and explains relevant jobs and internships, prioritizing postings from the last 72 hours. The MVP will support reviewing and saving recommended opportunities, suppressing duplicate listings, and choosing in-app or email delivery. Scans run every four hours while the app is running, with a manual Scan now option. The closed app does not scan or send email; on launch it shows saved results and runs one catch-up scan if the last successful scan is more than four hours old. For a selected job, users can review and accept an arrangement of existing confirmed resume bullets; the product does not generate new resume claims. Networking opportunities, hiring-manager and recruiter discovery, application essay assistance, and automated resume rewriting are outside the committed MVP. Interview and online-assessment tracking from the reference system are also excluded.

To keep the project manageable, we plan to limit retrieval to a small set of supported sources and focus on one complete profile-to-recommendation workflow. The product only needs to run on the team's laptops, so cloud deployment is not required. Source access, model quality and cost, resume extraction, and reliable scheduling and email delivery are the main feasibility risks to validate early. A fixed set of sample profiles and listings will support repeatable evaluation of matching explanations, factual grounding, freshness handling, and duplicate suppression, alongside a live retrieval demonstration. The team still needs to confirm source access and model availability before treating this scope as a validated implementation plan.

## Collaboration plan

Four members share one project and one AI-DLC v1.0.1 workflow. Each member claims one part in the table by adding a full name and NetID. Claiming a part means owning those tasks through the December 16, 2026 final project. The whole team still reviews and approves each stage. If two people want the same part, they divide the tasks inside that part and record the division in the table.

### Meeting frequency

The team meets twice a week through December 16, 2026. One meeting is a 90-minute working session. The other is a 45-minute review. The two weekly times are agreed in the group chat and then written into this section.

### How meetings are conducted

Meetings are online, with a shared screen on the repository and the coding agent. When all four members can be on campus for a session, that session is in person. One member runs the agent during the working session. The others stay in the session, answer questions, and review documents before the team approves a stage.

### Communication between meetings

Between meetings the team uses one group chat. A decision that changes scope, the model, the job sources, or the schedule is copied into the matching project document at the next working session, so the chat is not the only record.

### How the work is shared

Each member claims one of the four parts below. Implementation changes go through a branch and a pull request, and the reviewer is a member from a different part. Design decisions stay in one shared AI-DLC workflow, with the group's answers and approvals in a single record.

| Part | Focus | Claimed by (full name, NetID) |
|---|---|---|
| 1 | Process, repository, and AI-DLC record | |
| 2 | Product definition, stories | |
| 3 | Technical environment and local backend | Dennis Chen, (dc777)|
| 4 | Profile, matching quality, and evaluation | Alyssa Cohen, (ac2726) |

Tasks everyone shares:

- Attend both weekly meetings.
- Read the documents for a stage and approve them together.
- Answer the questions in the claimed part, and comment on the other parts.
- Request changes when a proposal does not fit the product.
- Keep API keys and private resume text out of the repository.
- Complete an individual peer evaluation for the final submission.

### Part 1 — Process, repository, and AI-DLC record

Choose this part to run the shared agent session, keep the record complete, and manage submission.

- Drive Construction one approved unit at a time, following the unit dependency order.
- Keep `aidlc-docs/audit.md` and `aidlc-docs/aidlc-state.md` current through functional design, non-functional requirements, non-functional design, infrastructure design, and code generation for every unit.
- Coordinate the build-and-test instructions and the record of test runs.
- Keep the final checklist: demo video, recorded presentation, repository, and peer evaluation.
- When the team pulls a stretch feature into scope, record that change through the workflow.

### Part 2 — Product definition, stories, and presentation

Choose this part to keep the written product consistent and to explain it at the end.

- Keep the README, the vision, and the requirements consistent when the team changes a decision.
- Check each Construction unit against the user stories and acceptance criteria.
- Write the demo script for the path from profile setup to a reviewed shortlist.
- Outline and help record the team presentation, including why an LLM fits, what the product does, and what was left out.
- If the team later adds them, write the stories for networking, recruiter or hiring-manager discovery, and interview or assessment tracking.

### Part 3 — Technical environment and local backend

Choose this part to own the stack, model setup, job retrieval, storage, scheduling, and delivery.

- Keep the technical environment document current after the team agrees on the provider, model, language, frameworks, local commands, prohibited libraries, and security basics.
- Implement the source adapters and the saved demo dataset used when a live source is unavailable.
- Implement persistence, the duplicate key, and saved statuses such as new, saved, hidden, applied, and rejected.
- Implement deterministic handling of freshness, eligibility, and unknown fields around the model output.
- Implement the scheduler, in-app delivery, and optional email delivery.
- Add unit and integration tests. Use fixtures when a live call would spend money or depend on the network.
- Write the local setup so any teammate can run the demo on a laptop.
- Add further source adapters, or read-only mail and calendar ingestion, only after the team moves that work into scope.

### Part 4 — Profile, matching quality, and evaluation

Choose this part to own the candidate profile, the explanations, the review screens, and the evaluation.

- Keep the profile fields specific: education, skills, projects, experience, preferences, and the source of each claim.
- Specify which extracted claims the user confirms before they are used, and how several resumes become one reviewed profile.
- With Part 2, record whether recombining existing resume bullets for a selected job is inside the user-reviewed product. Automated resume rewriting stays outside the MVP unless the whole team changes that decision.
- Implement resume and pasted-text extraction, with validation of the structured model output.
- Implement the profile review and correction screen.
- Implement fit explanations that cite listing evidence and profile claims, and that surface gaps and unknowns.
- Implement the shortlist review screen, including its empty and error states.
- Build the fixture set, run the evaluation, and summarize the results for the demo and the presentation.
- Add application-question preview, sample answers grounded in the confirmed profile, or user-reviewed bullet suggestions only after the team moves that work into scope.
