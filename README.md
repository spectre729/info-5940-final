# info-5940-final

## Team name and netID

Four members. Each person adds a full name and NetID. A GitHub login does not replace either one.

- Yiyang Cheng, yc3259
- Full name, NetID
- Full name, NetID
- Full name, NetID

## Coding Agent and AI-DLC version

AI-DLC v1.0.1.

Each member adds the coding agent they use:

- Agent:
- Agent:
- Agent:
- Agent:

## Problem and rationale for using LLMs

Students and recent graduates looking for jobs and internships often have to search across job boards, read lengthy descriptions, and decide whether each opportunity fits their background. Broad search results and recommendations can leave candidates spending time on roles that do not match their skills, experience level, or preferences. Repeating this process to find newly posted opportunities adds to the effort. Our project aims to reduce that manual screening by providing scheduled, personalized recommendations that prioritize jobs and internships posted within the last 72 hours.

An LLM is useful for comparing the varied language in job descriptions with the skills, projects, and experiences described in a candidate's resumes and profile. Candidates may maintain several resumes that emphasize different parts of their background, so the product will bring that information, pasted profile text, and manual additions into a user-reviewed profile. The LLM can use this context to identify relevant connections and explain why a role may be worth considering, including gaps or uncertain requirements. Recommendations should link to source listings, with posting dates and eligibility details grounded in those sources rather than assumed by the model. The goal is to help candidates make informed application decisions and spend less time repeatedly screening listings. Networking, recruiter discovery, and application essay assistance are stretch goals beyond the core discovery workflow.

## Planned LLM integration

The planned workflow uses an LLM to extract skills, projects, and experience from uploaded resumes and pasted profile text, then combine them with manually entered preferences into a profile the user can review and correct. During job discovery, the LLM will compare retrieved listings with this profile, prioritize potentially relevant opportunities, and generate explanations grounded in the candidate's experience and the listing. It should highlight missing qualifications or unclear requirements rather than inventing a match. The proposed agentic component will use a limited set of retrieval tools to search supported sources and inspect listing details before producing recommendations; specific sources and tool interfaces will be defined during design.

Scheduling, saved results, duplicate detection, and notification delivery will be handled by application code. Users will receive results in the app by default, with email delivery available as an option. Posting dates and other factual details must come from retrieved sources, with unavailable information marked as unknown. The planned LLM provider and model are still to be selected based on the team's available access, cost constraints, and tests of profile extraction and job-matching quality; this choice must be documented before the README is finalized.

## Project scope and feasibility

By the December 16 final-project deadline, our target is a locally running application for students and recent graduates that accepts multiple resumes, pasted profile text, and manual preferences; builds a user-reviewed candidate profile; and periodically retrieves and explains relevant jobs and internships, prioritizing postings from the last 72 hours. The MVP will support reviewing and saving recommended opportunities, suppressing duplicate listings, and choosing in-app or email delivery. The exact refresh frequency and behavior when the local application is closed remain to be defined. Networking opportunities, hiring-manager and recruiter discovery, application essay assistance, and automated resume rewriting are outside the committed MVP. Interview and online-assessment tracking from the reference system are also excluded.

To keep the project manageable, we plan to limit retrieval to a small set of supported sources and focus on one complete profile-to-recommendation workflow. The product only needs to run on the team's laptops, so cloud deployment is not required. Source access, model quality and cost, resume extraction, and reliable scheduling and email delivery are the main feasibility risks to validate early. A fixed set of sample profiles and listings will support repeatable evaluation of matching explanations, factual grounding, freshness handling, and duplicate suppression, alongside a live retrieval demonstration. The team still needs to confirm source access and model availability before treating this scope as a validated implementation plan.

## Collaboration plan

The four members share one project and one AI-DLC workflow. Each member claims one of the four parts below by writing a full name and NetID in the claim table. Claiming a part means drafting and later building those tasks. Stage approval stays with the whole team. If two people want the same part, they split the tasks inside that part and write the split in the table. Tasks left unclaimed stay in that part until someone claims them.

Repository accounts that can push, and therefore can claim a part, are spectre729, acohen974, young531zz, and dongyuunseo.

### Project instruction

INFO 5940 is one team project in two stages. The team uses an AI coding agent guided by AI-DLC v1.0.1 to design and build a product that itself uses an LLM. The committed rules for this repository are AI-DLC v1.0.1. The current layout is `AGENTS.md` plus `.aidlc-rule-details/`. A member who uses Cursor, Kiro, GitHub Copilot, Claude Code, or Amazon Q Developer also commits the v1.0.1 rule path for that agent.

The mid-semester milestone is due Tuesday, November 24, 2026, at 11:59 PM Eastern (America/New_York). It is worth 150 points, 15% of the course grade, with one submission for the team. The milestone completes the Inception phase: what to build and why. It includes requirements, user stories, application design, and units of work. Application code and the in-product model setup belong to the final project. The Canvas submission is one GitHub repository URL, and that URL needs to open in a private or incognito window without signing in. The repository contains the v1.0.1 rule files, this README, the vision document, the technical environment document, the Inception artifacts under `aidlc-docs/inception/`, `aidlc-docs/audit.md`, and `aidlc-docs/aidlc-state.md`.

The final project is due Wednesday, December 16, 2026, and is worth 35% of the course grade. The team completes Construction for every unit of work, then submits a product demo video, a recorded presentation, the repository, and the internal peer evaluation. The product runs locally on the team's laptops. Cloud hosting is optional. The planned model and provider are named in this README and in the technical environment document.

Working rules from the assignment:

- The team holds a real discussion of the problem, the users, and why an LLM fits, and then confirms that decision together before approving requirements.
- One member runs the coding agent and commits the Inception artifacts. The other members join the session, answer questions, and review documents.
- The team runs one shared AI-DLC workflow. `audit.md` is the record of the shared answers and approvals.
- Members who want to commit outside the live session use branches and pull requests. Inception artifacts still belong to the single shared record.
- Every AI-DLC question gets an `[Answer]:`. The team reads each document and requests changes when a proposal does not fit the product.
- At each approval gate, the session starts a fresh context. An exploratory question begins with "Do not update any documents." The session driver then adds the audit entry.
- Corrections go through the workflow. The team asks the agent to repair a missing audit entry.
- API keys, provider secrets, and private resume text stay out of git.
- The milestone stops after Units Generation is approved, before Construction.
- The milestone rubric scores five areas, 30 points each: the LLM product proposal and scope in this README, the two input documents, the AI-DLC process and record, the Inception artifacts, and clarity. Clarity requires every full name, every NetID, this collaboration plan, and a repository that is easy to follow.

### How the team meets and shares work

On Tuesday, November 24, 2026, the team holds one online working session and stays with it through the Inception approvals and the push. The member who claims Part 1 runs the agent and shares the screen. The session includes a short confirmation of decisions already drafted: students and recent graduates as the audience, scheduled recommendations that prioritize postings from the last 72 hours, a user-reviewed profile built from resumes, pasted profile text, and manual additions, in-app results as the default with optional email, and networking, recruiter discovery, essay help, automated resume rewriting, and interview or online-assessment tracking as stretch or excluded scope.

From November 25 through December 16, the team meets online twice a week: one 90-minute build session and one 45-minute review session. At the end of the November 24 session, the team writes the two weekly times into this section. A meeting is in person when all four members can be on campus for it. Otherwise it stays online.

Between meetings, the team uses one group chat. A decision that changes scope, the model, the sources, or the schedule is copied into the matching AI-DLC question file or the vision open-questions table at the next session. During Construction, code changes use branches and pull requests, and the reviewer is a member from a different part.

### Claim table

| Part | Focus | Claimed by (full name, NetID) | Notes |
|---|---|---|---|
| 1 | Process, repository, and AI-DLC record | | |
| 2 | Product definition, stories, and presentation | | |
| 3 | Technical environment and local backend | | |
| 4 | Profile, matching quality, and evaluation | | |

### Tasks everyone shares

- Join the November 24 working session and the later build and review meetings.
- Confirm the problem, the audience, and the LLM rationale before requirements approval.
- Read the vision and the technical environment before approving them.
- Answer the questions in the claimed part, and comment on the other parts.
- Request changes when a proposal does not match the product, then approve the stage.
- Keep credentials and private resume text out of the repository.
- For the final submission, complete an individual peer evaluation.

### Part 1 — Process, repository, and AI-DLC record

Choose this part to run the shared agent session, keep the record complete, and manage submission.

Milestone, due November 24, 2026, 11:59 PM Eastern:

- Confirm that all four teammates have access to the repository.
- Confirm the committed AI-DLC v1.0.1 rules, and add the rule path for any other agent a teammate uses.
- Record the agents and AI-DLC v1.0.1 in this README.
- After the team reviews the vision and technical environment, start the shared workflow from those two documents.
- Collect the group's answers and enter every `[Answer]:`.
- Keep `aidlc-docs/audit.md` as a timestamped record of prompts, answers, and approvals.
- Update `aidlc-docs/aidlc-state.md` as each stage finishes, is skipped, or is in progress.
- Start a fresh context at each approval gate.
- Log exploratory questions after they are asked with "Do not update any documents."
- Record the team's opt-in or opt-out for the security, resiliency, and property-based testing extensions.
- Check that requirements, stories, the execution plan, application design, and the units files were produced through AI-DLC and match the record.
- After the team approves Units Generation, tell the agent to stop before Construction.
- Check that the repository URL opens without signing in.
- Submit that URL on Canvas.

Final project, through December 16, 2026:

- Drive Construction one approved unit at a time, following `unit-of-work-dependency.md`.
- Keep the audit and state files current through functional design, NFR requirements, NFR design, infrastructure design, and code generation for every unit.
- Coordinate the build-and-test instructions and the record of test runs.
- Keep the final checklist: demo video, recorded presentation, repository, and peer evaluation.
- If the team later pulls a stretch feature into scope, record that change through the workflow.

### Part 2 — Product definition, stories, and presentation

Choose this part to own the written product: who it is for, what the MVP includes, and how the team explains it.

Milestone, due November 24, 2026, 11:59 PM Eastern:

- Collect four full names and NetIDs and add them under Team name and netID.
- Lead the team confirmation of the problem and the reason for using an LLM.
- Review the drafted README sections on the problem, the planned LLM integration, and the scope, and edit any point the team does not accept.
- Complete `aidlc-docs/inputs/vision.md`: users, core journey, MVP features, exclusions, LLM and data boundaries, success criteria, and open questions.
- Keep the vision consistent with this README.
- Carry the decisions already made into the requirements: students and recent graduates; uploaded resumes and pasted profile text; one user-reviewed profile that preserves the source of each claim; scheduled discovery that prioritizes the last 72 hours; in-app results by default and optional email.
- Write the exclusion list: networking, hiring-manager and recruiter discovery, application essays, automated resume rewriting, interview and online-assessment tracking, automatic applications, and automatic outreach.
- With Part 4, decide whether suggesting a recombination of existing resume bullets for a selected job is inside the user-reviewed MVP or stays a stretch goal. Automated rewriting remains outside the MVP unless the whole team changes that decision.
- Draft a student persona and a recent-graduate persona with specific goals and constraints.
- Draft user stories with acceptance criteria for profile setup, refresh, grounded explanations, saving a shortlist, duplicate suppression, and the delivery choice.
- Review the requirements, personas, and stories with the team before approval.

Final project, through December 16, 2026:

- Check each Construction unit against the stories and acceptance criteria.
- Write the demo script for the path from profile setup to a reviewed shortlist.
- Outline and help record the team presentation, including the LLM rationale, the scope, and the excluded work.
- If the team later adds them, write the stories for networking, recruiter or hiring-manager discovery, and interview or assessment tracking.

### Part 3 — Technical environment and local backend

Choose this part to own the stack, the model setup, job retrieval, storage, scheduling, and delivery mechanics.

Milestone, due November 24, 2026, 11:59 PM Eastern:

- Propose the LLM provider and exact model, including who has access, the cost or hardware limit, and how the team will test profile extraction and matching quality. The assignment allows a hosted API or a local model such as one served by Ollama.
- After the team agrees, name that provider and model in this README and in `aidlc-docs/inputs/technical-environment.md`.
- Choose the language and version, package manager and lockfile, UI framework, API framework, validation library, persistence, test framework, and formatter or linter.
- Document local execution: install command, start command, test command, URL and port, data location, and seed data for a demo that still runs when a live source or the model is unavailable.
- Complete the prohibited-libraries table with a reason and an approved alternative for each entry.
- Write the security basics: secret storage, personal-data minimization and deletion, validation and display of retrieved text, treatment of external text as untrusted model input, tool permissions, local network exposure, and log redaction.
- Replace the sample endpoint, function, and test with examples in the chosen stack.
- Propose the small set of listing sources, the access method, rate limits, and a saved demo dataset.
- Propose the refresh frequency and the behavior while the local app is closed.
- Lead the technical side of application design: components, methods, and dependencies.
- Review the units of work and their dependency order against what the team can build by December 16.

Final project, through December 16, 2026:

- Implement the source adapters and the fixture fallback.
- Implement persistence, the duplicate key, and saved statuses such as new, saved, hidden, applied, and rejected.
- Implement deterministic handling of freshness, eligibility, and unknown fields around the model output.
- Implement the scheduler and in-app delivery.
- Implement optional email delivery.
- Add unit and integration tests for that behavior. Use fixtures or mocks when a live call would spend money or depend on the network.
- Write the local setup so any teammate can run the demo on a laptop.
- Add further source adapters, or read-only mail and calendar ingestion, only after the team moves that work into scope.

### Part 4 — Profile, matching quality, and evaluation

Choose this part to own the candidate profile, the quality of the explanations, the review experience, and the evaluation.

Milestone, due November 24, 2026, 11:59 PM Eastern:

- Specify the profile fields: education, skills, projects, experience, preferences, and the source of each claim.
- Specify upload of more than one resume, pasted profile text, and manual additions, and specify which extracted claims the user confirms before they are used.
- Specify how several resumes become one reviewed profile.
- With Part 2, write the decision on user-reviewed recombination of existing bullets for a selected job.
- Specify each recommendation the user sees: source link, posting freshness, work arrangement and eligibility when the source provides them, the matching experience, missing qualifications, and an explicit unknown where a fact is absent.
- Specify shortlist actions: save, hide, and the statuses the team keeps.
- Draft the evaluation fixtures: a fresh posting, a stale posting, a missing date, a duplicate listing, an already seen listing, an unclear requirement, and a strong skill overlap.
- Propose demo targets for factual grounding, freshness labels, and duplicate suppression.
- Write those behaviors into story acceptance criteria with Part 2.
- Review the application design for the profile and explanation flow.

Final project, through December 16, 2026:

- Implement resume and pasted-text extraction, with validation of the structured model output.
- Implement the profile review and correction screen.
- Implement fit explanations that cite listing evidence and profile claims, and that surface gaps and unknowns.
- Implement the shortlist review screen and its empty and error states.
- Build the fixture set, run the evaluation, and summarize the results for the demo and the presentation.
- Add application-question preview, sample answers grounded in the confirmed profile, or user-reviewed bullet suggestions only after the team moves that work into scope.
