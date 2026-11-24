## Workflow start / Workspace Detection / Requirements Analysis
**Timestamp**: 2026-11-19T17:18:08Z
**User Input**: "Good. Let's come up with a plan for this project. "
**AI Response**: Displayed the complete welcome message. Read local common and stage rules, extension opt-in files, README, and assignment PDF. Workspace is greenfield; Reverse Engineering is skipped. Proposed a career opportunity assistant and dated planning outline, created state and nine requirements questions, and deferred final requirements until team answers. Input documents remain to be prepared and reviewed. No application code changed. Installed release verification remains pending.
**Context**: Earlier repository-discovery conversation predates workflow initialization; original timestamps were not recorded and no historical approval is inferred. Initial content validation caught a question-count assertion before any files were written; corrected the validation and used plain Markdown without diagrams or embedded code requiring parsing.

---

## Requirements answer gate
**Timestamp**: 2026-11-19T17:18:08Z
**User Input**: No additional user input.
**AI Response**: Present the proposed plan and questions; request all nine answers in the question file. Explain that .aidlc-rule-details/inception/requirements-analysis.md Step 6 explicitly requires stopping for answers before final requirements. Summarize the November 24 Inception deadline and December 16 final deadline. No extension enablement or Requirements Analysis completion claimed.
**Context**: Waiting for team scope, access, technology, collaboration, and extension decisions. Formal execution plan follows requirements and stories.

---
## Requirements Analysis - input templates
**Timestamp**: 2026-11-19T17:26:28Z
**User Input**: "Let's create a template for the vision and technical environment"
**AI Response**: Created aidlc-docs/inputs/vision.md and aidlc-docs/inputs/technical-environment.md as fill-in project input templates aligned with assignment sections. Left undecided choices as TODO and clearly labeled illustrative career-assistant/Python examples. Parsed both JSON examples and Python examples and executed the illustrative test successfully before writing. Updated plan checkbox and state without marking inputs reviewed or advancing the requirements gate. Final reply links both templates and states that choices remain open.
**Context**: User explicitly requested templates; no final requirements, team approvals, or extension decisions inferred. Full extension rules remain deferred pending opt-in answers; this supporting task does not complete a workflow stage.

---
## Requirements Analysis - README part 1 discussion
**Timestamp**: 2026-11-19T17:37:40Z
**User Input**: "Looks good. I want to start with writing up the README file. We'll first work on part 1: **Problem and rationale for using LLMs**


The problem is that most job boards are either just a comprehensive list or recommends jobs that aren't a good fit for candidates. The idea for the MVP is to use an LLM to find relevant and recently posted jobs and internships for these candidates. I want this primarily for students and other job seekers so they can get updates on new jobs that they should apply to. Bonus features include finding relevant networking opportunities, hiring managers/recruiters, and preview on short essay questions and generate a sample template.&#x20;

Take a look at my input and see if there's any feedback/questions/concerns that you have for me before writing it to the README"
**AI Response**: Reviewed README and workflow context. Prepared four focused clarification questions in inception/requirements/readme-part-1-questions.md. Feedback: describe the observed search burden without an unsupported claim about most boards; explain semantic matching and evidence-based fit explanations as the LLM rationale; obtain freshness from listing sources; define primary audience and update behavior; treat bonus features as stretch goals pending confirmation. README remains unchanged. Question Markdown validated before writing.
**Context**: User explicitly requested feedback before drafting. This input narrows the proposed product but does not answer all earlier requirements questions or constitute stage approval. Optional extension decisions remain pending.

---
## Requirements Analysis - answer review and existing system
**Timestamp**: 2026-11-19T17:49:49Z
**User Input**: "I added my answers to the file. Take a look and share any questions that you may have. As a side note, I have a similar setup where a scheduled task looks for relevant roles, networking opportunities, and a summary on what tasks I have, such as upcoming interviews, OAs, etc. This setup may be useful for you to understand if you are interested. If possible, you can view the chatgpt memory, and if not, you can generate a prompt that I can give to chatgpt to summarize my existing job search system. "
**AI Response**: Read all four answers, retaining original wording below. Audience and stretch-goal choices are clear. Requested clarification of profile ingestion, combined skills, and scheduled delivery in a follow-up file. Inspected available tool capabilities: no saved ChatGPT memory reader is exposed in this session. Created a copyable prompt to summarize the existing system without inventing inaccessible facts or changing tasks. Existing interview/OA tracking is reference context, not automatically added to MVP scope. Consulted OpenAI docs capability-check instructions and writing-style instructions; writing search returned no suitable prose reference, so prompt follows user-supplied language. README unchanged; no stage advanced. Plain Markdown validated before file creation.
**Context**: Awaiting remaining behavioral decisions and optional system summary. Four-hour reference cadence is not treated as an explicit MVP choice. No requirements-gate approval inferred.

### User-edited answer file, verbatim

# README part 1 clarification

Purpose: settle the problem statement and LLM rationale before drafting the README. Technical implementation choices can wait. You may also respond in chat referencing these question numbers.

## Question 1: Initial audience

Who is the primary audience for the MVP?

A) Students and recent graduates seeking internships and entry-level jobs; other job seekers are a future audience.

B) Students and job seekers at all experience levels from the start.

C) Other (describe after the answer tag).

[Answer]: The primary audience that I have in mine is in group A: students and recent graduates. mid-level and senior level job seekers can be something we do in the future

## Question 2: Meaning of relevance

What information should define a good match? Add any must-have criteria and one concrete example of a strong versus poor match.

A) Skills, experience, and projects from a resume/profile, combined with explicit role, location, and work-eligibility preferences.

B) Manually entered skills and preferences, without resume upload in the MVP.

C) Other (describe after the answer tag).

[Answer]: It should be a combination of A and B, with a resume/linkedin profile as the primary source. Users might maintain multiple resumes so we should all the skills a user has. 

## Question 3: Updates and recency

What does getting updates mean for the MVP? Specify the intended recent-posting window, if already decided. New since the last search and recently posted are distinct concepts.

A) An on-demand refresh that highlights newly discovered listings within a defined posting window.

B) A scheduled in-app digest of matching new listings.

C) Scheduled email or other external notifications.

D) Other (describe after the answer tag).

[Answer]: For the MVP, it should be a scheduled feature where we prioritizes new posting within the last 72 hours. For references, I currently have a scheduled task of 4 hours that does this. 

## Question 4: Bonus features

How should networking, recruiter discovery, and essay support be positioned? For any option, clarify whether essay preview means displaying actual application prompts, explaining them, or drafting sample responses from the candidate's real experience.

A) All are stretch goals outside the committed MVP.

B) One is part of the MVP; name it and specify its behavior, with the others as stretch goals.

C) Other (describe after the answer tag).

[Answer]:
A: all should be stretch goals that can be added time permitting. 

---
## Requirements Analysis - follow-up answer review
**Timestamp**: 2026-11-24T14:21:21Z
**User Input**: "ok, so I answered the follow-up questions, let me know if there is anything else from me"
**AI Response**: Read all three follow-up answers. Confirmed uploaded resumes/pasted profile text, a combined user-reviewed profile, and both in-app (default) and optional email delivery. No further input is needed for README part 1. Resume bullet tailoring may expand earlier scope and will need definition later; exact cadence and app-closed scheduling behavior remain unconfirmed, but do not block the problem/rationale section. Existing ChatGPT system summary is optional context. README remains unchanged; no workflow stage or approval gate advanced. Audit entry uses plain Markdown, with no diagrams or embedded code requiring parsing.
**Context**: Review requested before README drafting; accepted natural-language answers are semantically clear despite not being bare option letters. No automatic inference that resume generation is approved as an MVP feature. Extension decisions remain pending.

### User-edited follow-up answers, verbatim

# README part 1 follow-up questions

The first answers establish students/recent graduates as the initial audience, resume/profile-based matching with manual additions, scheduled discovery prioritizing postings from the last 72 hours, and all bonus features as stretch goals. The existing four-hour task is a reference, not yet a confirmed MVP frequency. These follow-ups clarify remaining behavior without changing earlier answers.

## Question 1: Profile input

How should the MVP receive resume and LinkedIn information?

A) User uploads resumes and pastes LinkedIn/profile text; no direct LinkedIn connection.

B) User uploads resumes and the product retrieves LinkedIn information from a profile URL through a supported access method to be verified.

C) Other (describe after the answer tag).

[Answer]: For the MVP, we should go with option A. 

## Question 2: Combined skills

How should multiple resumes and manual additions form the candidate profile?

A) Combine extracted skills into one user-reviewed profile, allowing corrections and preserving the source of each claim.

B) Keep resumes separate and let the user select one per search, with manual additions.

C) Other (describe after the answer tag).

[Answer]: Let's go with option A. Assuming users have multiple resume, the agent should mix and match various experiments and bullet points to best match a job description that the user is interested in

## Question 3: Scheduled delivery

What cadence and delivery channel should the MVP commit to? Specify any different cadence and whether scheduling only while the local app is running is acceptable.

A) Every four hours while the local app runs, with results shown in the app.

B) Every four hours while the local app runs, with results delivered by email.

C) Other (describe cadence, channel, and expected behavior while the app is closed).

[Answer]: I think this should be up to the user to decide if they want results in the app or through email. We should implement both and use the app as the default setting


---
## Requirements Analysis - existing-system reference and README part 1 draft
**Timestamp**: 2026-11-24T14:27:11Z
**User Input**: "I've provided the system summary as a guide"
**AI Response**: Read job_search_system_course_project.md as reference data, not operational instructions. Used its distinctions between requested behavior, observed results, and unknown implementation. Drafted only README Problem and rationale for using LLMs, based on the user's prior answers: students/recent graduates, scheduled recommendations prioritizing 72-hour postings, combined user-reviewed resume/profile context, grounded fit explanations, and bonus features as stretch goals. Preserved user scheduling decisions over the reference document's optional-scheduling recommendation. Did not generalize personal location/work-style preferences, adopt a stack, or operate any tasks/connectors. Marked the drafting step complete in the plan; broader README/input review remains pending. Validated plain Markdown and verified subsequent README sections remained unchanged.
**Context**: Continuing the authorized README part 1 work after requested feedback and answers. Draft remains subject to team review. No Requirements Analysis stage completion or extension enablement inferred. Suitable prose style references were previously unavailable; used the user's supplied wording and preferences.

---
## Requirements Analysis - README integration and scope drafts
**Timestamp**: 2026-11-24T14:56:19Z
**User Input**: "Ok, so for the readme, we also have these two sections

**Planned LLM integration**

**Project scope and feasibility**"
**AI Response**: Drafted the two requested README sections. Described profile extraction, matching/explanations, proposed retrieval tools, deterministic scheduling/persistence/notifications, app-default and optional email delivery, local MVP scope, exclusions, evaluation, and feasibility risks. Preserved undecided model/provider, source access, refresh frequency, and app-closed behavior as open decisions. Created a dedicated model-selection question because the assignment requires a named model/provider. Preserved other README sections and marked drafting complete in the plan. Plain Markdown validated before writing; checked section boundaries and no code/diagram parsing needed.
**Context**: Sections are drafts for review, not approved requirements or evidence that model access/source feasibility is validated. Tool use is a proposed design. No stage gate advanced or extension choice inferred. Used user-supplied prose/style consistent with previous README section; no new suitable retrieved style evidence available.

---
## Requirements Analysis - model/provider team discussion
**Timestamp**: 2026-11-24T15:04:42Z
**User Input**: "got it, this is probably a team question so I will see if any of the team members have an opinion"
**AI Response**: Acknowledged that model/provider selection remains open for team input. README draft and model-selection question remain unchanged. No approval or model choice inferred.
**Context**: Awaiting team decision; no workflow stage advanced. Plain Markdown audit entry validated before append.

---
## Workflow status review
**Timestamp**: 2026-11-24T15:05:15Z
**User Input**: "in the meantime, what other step is missing?"
**AI Response**: Inspected README, state, input templates, question files, and artifact inventory. Identified missing README team/agent/collaboration details, incomplete vision and technical-environment templates, unresolved requirements/source/scheduling/evaluation/extension choices, and absent formal requirements, stories/personas, execution plan, application design, and units/dependency/story-map artifacts. Recommended completing the vision next using existing answers, with open decisions explicit, while awaiting model input. Noted the November 24 milestone is today and requires full Inception, with Construction deferred. Existing answered clarifications should be reconciled into requirements rather than asked again. No stage advanced or document approval inferred; plain Markdown entry validated before append.
**Context**: Read-only status review apart from mandatory audit append. Installed AI-DLC v1.0.1 verification and final commit/push/accessibility/submission checks remain pending.

---

## Requirements Analysis - collaboration plan
**Timestamp**: 2026-11-24T18:51:32Z
**User Input**: "https://github.com/spectre729/info-5940-final/tree/main for this project, there are four people,in collaboration plans, please list all possible tasks and seperate them into four parts for team members to choose,and the project instruction

Mid-semester Milestone: Complete the AI-DLC Inception Phase
Due: Tuesday, November 24, 2026, 11:59 PM · Points: 150 (15% of the course grade) · One submission per team

About the project
This semester’s project is one team project, built in two stages. Your team will use an AI coding agent, guided by the AI-Driven Development Lifecycle (AI-DLC v1.0.1), to design and build a product that itself uses LLMs. In other words, you use LLMs to build a product that leverages LLMs.

Choose a problem you care about. Start from a problem you find interesting or know well, from your studies, work, hobbies, or community, and that you’re curious to apply AI to. The product can be anything, as long as LLMs are part of how it works. We especially encourage products that use agentic patterns. A basic LLM feature makes one call and returns text, such as a summary or an answer. An agent goes further: the LLM decides what steps to take, calls tools (for example, searching a database, calling an API, or running code), and uses the results before it responds. A focused MVP (minimum viable product) is a good target for your project. An MVP is the smallest version of your product that still solves the core problem for your users: the few features that matter most, each one working the way a real user would need it to. You can leave “nice-to-have” features for later, and list them as out of scope in your vision document. During , AI-DLC will help you split your MVP into manageable units of work.Inception

AI-DLC is AWS’s methodology for AI-driven software development: the AI creates plans, asks clarifying questions, and builds, and your team reviews and approves each step. It has three phases: (what to build and why), (how to build it), and (a placeholder in v1. This phase will not be required for this project).InceptionConstructionOperations

Mid-semester Milestone (due Tuesday, November 24, 15% of the course grade): set up AI-DLC in your team repository, write your and your and , then complete the phase.READMEvisiontechnical environment documentsInception
Final Project (due Wednesday, December 16, 35% of the course grade): complete the phase for every unit of work, then submit a product demo video, a recorded presentation, your team repository, and the internal team-based peer evaluation.Construction
What this milestone requires from you
By the deadline, your team will have used AI-DLC v1.0.1 to complete the phase, which determines what to build and why: requirements, user stories, application design, and units of work. You do not need to write any application code or set up the LLM inside your product yet; that happens in the final project.Inception

You will submit one link to your team’s GitHub repository. It must contain:

The for your coding agentAI-DLC v1.0.1 rule files
A with your names, NetIDs, project overview, and collaboration planREADME
Your and vision documenttechnical environment document
The artifacts AI-DLC generates in Inceptionaidlc-docs/inception/
The AI-DLC record: and aidlc-docs/audit.mdaidlc-docs/aidlc-state.md
Choosing your tools
Your AI coding agent
Please use the AI coding agent of your choice, based on your availability (this choice will not be evaluated), such as Claude Code, Kiro, Cursor, GitHub Copilot, Amazon Q Developer, or OpenAI Codex, as long as it can load the AI-DLC v1.0.1 rules and you apply the framework correctly. Teammates can use different agents, as long as the rule files for each agent your team uses are installed and committed correctly.

Several agents offer free plans or limited free usage, and GitHub Copilot is free for verified students through GitHub Education. If you run out of free usage, Ollama can run some coding agents, including Claude Code and Codex, with free open models. See https://docs.ollama.com/integrations/claude-code and https://docs.ollama.com/integrations/codex. Local models need tool support and a long context window, and results depend on the model you choose.

The LLM inside your product
Please use the LLMs of your choice, based on your availability (the specific model or provider you choose will not be evaluated), as long as they work for your proposed product. The LLMs inside your product can come from any provider. For example, you can run free open models locally with Ollama, and your product can call them through Ollama’s API, including an OpenAI-compatible endpoint.

Download Ollama: https://ollama.com/download
Browse models: https://ollama.com/library
Get started: https://docs.ollama.com/quickstart
OpenAI-compatible API: https://docs.ollama.com/openai
You do not need to set this up for the milestone, but name your planned model and provider in your and . Choosing and setting up a model is part of the project, so read the documentation and try it early.READMEtechnical environment document

AI-DLC v1.0.1 resources
Use AI-DLC v1.0.1 only. The main branch of the AI-DLC repository is now version 2, so use these v1.0.1 links:

Release page and rules download (): https://github.com/awslabs/aidlc-workflows/releases/tag/v1.0.1ai-dlc-rules-v1.0.1.zip
Setup instructions for each coding agent: https://github.com/awslabs/aidlc-workflows/blob/v1.0.1/README.md
Working with AI-DLC: https://github.com/awslabs/aidlc-workflows/blob/v1.0.1/docs/WORKING-WITH-AIDLC.md
Writing your input documents (start here): https://github.com/awslabs/aidlc-workflows/blob/v1.0.1/docs/writing-inputs/inputs-quickstart.md
Example vision document: https://github.com/awslabs/aidlc-workflows/blob/v1.0.1/docs/writing-inputs/example-minimal-vision-scientific-calculator-api.md
Example technical environment document: https://github.com/awslabs/aidlc-workflows/blob/v1.0.1/docs/writing-inputs/example-minimal-tech-env-scientific-calculator-api.md
Every artifact AI-DLC can generate: https://github.com/awslabs/aidlc-workflows/blob/v1.0.1/docs/GENERATED_DOCS_REFERENCE.md
The methodology (AWS DevOps Blog): https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/
How to work as a team
The phase revolves mostly around group discussion and documentation rather than code. AI-DLC is designed for the whole team to make decisions together, so plan to work in shared sessions.Inception

Choose one team member to create the repository, run the coding agent, and commit the changes for the phase. Everyone else joins each working session and takes part in the decisions. Discussing ideas, answering the AI’s questions, and reviewing documents are all contributions that each member should make; please note, no programming is needed at this stage.Inception
If your team is comfortable with GitHub and source control, other members can commit too, for example through branches and pull requests.
Run one AI-DLC workflow together. Please do not have each member run AI-DLC separately. The record in should show your team’s shared answers and approvals, which will be evaluated.audit.md
A few more points:

You may use AI to help write your and input documents. Be sure to review what it produces, as your team is responsible for the content.README
If the AI asks something you don’t know, that is an opportunity to use AI itself, and preferably other resources on the web and library to learn more. That is part of the project (and the process). Most questions are about the product. The stage asks more technical questions, for example, how the code is organized and tested, so make sure your more technical members are involved in leading some of those decisions.InceptionApplication Design
Start as early as you can. The phase asks many questions and stops for many approvals.Inception
What to complete
Step 1. Set up your team repository and AI-DLC
One team member creates a GitHub repository for the project and adds every teammate as a collaborator. See the following page for more guidance on this: https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository
Download from the release page and unzip it outside your project. Copy the rules to where your agent reads them, following the at the v1.0.1 tag: ai-dlc-rules-v1.0.1.zipREADME
Claude Code: core rules go to (a copy of ); rule details go to CLAUDE.mdcore-workflow.md.aidlc-rule-details/
Kiro: core rules go to ; rule details go to .kiro/steering/aws-aidlc-rules/.kiro/aws-aidlc-rule-details/
Amazon Q Developer: core rules go to ; rule details go to .amazonq/rules/aws-aidlc-rules/.amazonq/aws-aidlc-rule-details/
Cursor: core rules go to (see the for the header); rule details go to .cursor/rules/ai-dlc-workflow.mdcREADME.aidlc-rule-details/
GitHub Copilot: core rules go to ; rule details go to .github/copilot-instructions.md.aidlc-rule-details/
OpenAI Codex and other agents: core rules go to ; rule details go to AGENTS.md.aidlc-rule-details/
Commit the rule files. The AI-DLC recommends version-controlling them.README
Check that it works: start a session with “Using AI-DLC, …”. The agent should show the AI-DLC welcome message and create an folder. If it doesn’t, the rules are not loaded; check the file locations.aidlc-docs/
AI-DLC writes all of its artifacts to at the repository root. Application code goes at the repository root, never inside . Do not commit API keys or other secrets to your repository.aidlc-docs/aidlc-docs/

Throughout the milestone, keep the AI-DLC record complete. Once you start the workflow, AI-DLC automatically creates and updates two files. records every input, AI response, and approval with a timestamp, and tracks which stages are complete, skipped, or in progress. These files are how graders see that you followed AI-DLC.aidlc-docs/audit.mdaidlc-docs/aidlc-state.md

Commit both files with your work.
Check them at each gate. If something wasn’t logged, ask the agent to add it rather than editing the file yourself.
Follow Working with AI-DLC:
reset the context at each gate
start exploratory questions with “Do not update any documents.” The agent may then leave the question out of . If it does, ask it to add the entry once you’re done.audit.md
fix problems through the workflow rather than by editing files by hand
Step 2. Write your README
Your is your team’s own overview of the project: what you are building, why, and how you will work. It must include:README.md

Every team member’s full name and NetID
The coding agent or agents you use, and the AI-DLC version (v1.0.1)
About 4–6 paragraphs (roughly 1–2 pages) covering these four areas:
Problem and rationale for using LLMs: the problem your product addresses, who it is for, and why an LLM is an appropriate way to solve it.
Planned LLM integration: how LLM capabilities will be part of the product, which features depend on them, whether you plan to use agents or tools, and which model or provider you plan to use.
Project scope and feasibility: what the finished product will do by the final project deadline. It should be a meaningful course project, not a single minor feature, while remaining achievable.
Collaboration plan: how often your team will meet, how meetings will be conducted (in person or online), how you will communicate between meetings, and how you will share the work.
Areas 1–3 are graded under criterion A. Please dedicate at least one full team meeting to thoroughly discussing the problem you aim to address with your proposed LLM-integrated product. The names, NetIDs, and collaboration plan are graded under criterion E.

Step 3. Write your two input documents
AI-DLC recommends preparing two documents before starting: a vision document and a technical environment document. Start with the inputs quickstart, then look at the worked examples (links above). The quickstart also describes a “minimum viable input” if you want to start quickly and fill in details later. Make sure to commit both documents to your repository.

Vision document

What you are building and for whom
MVP features in scope
Features explicitly out of scope
Open questions
Technical environment document

Language and version, package manager, and framework
Cloud provider and deployment model
Test framework
A prohibited-libraries table, with a reason and an alternative for each entry
Security basics
At least one example each of a typical endpoint, function, and test
Your product only needs to run locally. You do not need to deploy it to the cloud or host it online; it only has to run on your team’s laptops, so you can demo it. Make your technical choices with that in mind. In the “Cloud provider and deployment model” section, say that the product runs locally and how it runs (for example, a local web app that calls a model running in Ollama). Your product can still call a hosted LLM provider’s API if you choose one.

A document is complete when every section above has specific content for your product, not template text or placeholders. Both documents should be reviewed and agreed by the whole team before you start Step 4.

Step 4. Complete the Inception phase
Meet as a team and start the workflow as the AI-DLC docs describe, for example:

Using AI-DLC, I want to start a new project. Please read [your vision document] and [your technical environment document], then begin the AI-DLC workflow.

AI-DLC then walks you through the stages its execution plan includes. At each stage it asks clarifying questions in a question file, which you answer, and it stops for your approval: Request Changes or Approve & Continue. Work through the stages together:Inception

Answer every question deliberately. Never leave an blank.[Answer]:
Review each document as a team before you approve it. If a proposal doesn’t fit your product, push back: ask questions and request changes. This engagement is part of criterion C.
Give it real thought. The quality of your requirements, stories, and personas reflects the effort you put in, and is graded under criterion D.
AI-DLC generates these artifacts in :aidlc-docs/inception/

Requirements Analysis: and , with every filled inrequirements/requirements.mdrequirements/requirement-verification-questions.md[Answer]:
User Stories: and user-stories/stories.mduser-stories/personas.md
Workflow Planning: plans/execution-plan.md
Application Design: the files in application-design/
Units Generation: , , and application-design/unit-of-work.mdunit-of-work-dependency.mdunit-of-work-story-map.md
Stop after Units Generation. Its approval prompt offers to continue to the phase. For the milestone, approve the units and tell the agent to stop before . You will start in the final project.ConstructionConstructionConstruction

How to submit
Commit and push all your work to your team’s GitHub repository by the deadline, and submit the GitHub repository URL on Canvas. Please make sure that the link opens in a private or incognito browser window without signing in.

Rubric (150 points)
A. LLM-integrated product proposal and its scope: 30 points
B. AI-DLC input documents: 30 points
C. AI-DLC process and record: 30 points
D. Inception artifacts: 30 points
E. Clarity: 30 points
Total: 150 points
Each criterion is 20% of the milestone grade and is graded separately. Points within a level are at the grader’s discretion. 

A. LLM-integrated product proposal and its scope (30 points)
This criterion evaluates the rationale for using LLMs in your proposed product, your plan for integrating them, and the project’s scope, as described in areas 1–3 of your .README

Excellent (27–30): The provides a clear and compelling rationale for why LLMs are well-suited to the identified problem. It outlines a well-defined plan for integrating LLM capabilities into the product. The scope is ambitious enough to be a meaningful course project, rather than one minor feature, while remaining achievable by the final project deadline.README
Good (23–26): The gives a reasonable rationale for using LLMs to address the identified problem. It describes how LLM capabilities will be integrated, although some details need further clarification. The proposed scope is generally appropriate and feasible for a course project.README
Fair (19–22): The rationale for using LLMs is limited or unclear, making it difficult to understand why LLMs are appropriate for the problem. The integration plan lacks detail. The scope may be too narrow to be a meaningful course project, or too broad to be achievable by the final project deadline.
Poor (0–18): There is little or no justification for using LLMs, or the proposed use of LLMs is not meaningfully connected to the problem. The integration plan is missing, vague, or impractical. The scope is substantially too limited or unrealistic for the course timeline.
B. AI-DLC input documents (30 points)
This criterion evaluates the quality of the and you provide to start AI-DLC.visiontechnical environment documents

Excellent (27–30): Both documents are complete and cover all required sections. The content is specific, detailed, and actionable, with clear requirements, relevant technical information, and useful example code that AI-DLC can follow.
Good (23–26): Both documents are complete and cover all required sections, but some sections are generic, vague, or not detailed enough to guide AI-DLC well.
Fair (19–22): One or both documents are incomplete, with some required sections missing or insufficiently addressed. The content offers only partial guidance for AI-DLC.
Poor (0–18): One or both documents are missing.
C. AI-DLC process and record (30 points)
This criterion evaluates whether you set up and used AI-DLC as designed, using and as evidence of how your team worked with the agent. We look at three things:aidlc-docs/audit.mdaidlc-docs/aidlc-state.md

Setup: the rule files are installed and committed, so your agent follows the workflow.AI-DLC v1.0.1
Following AI-DLC: your Inception artifacts were produced through the AI-DLC workflow. A complete and consistent record shows each stage, your answers, and your approvals, and matches the artifacts in your repository. A record is incomplete or inconsistent when artifacts exist that the record does not show being produced: for example, if the agent was told to skip the process and just write the documents, if artifacts were produced with another tool outside the workflow, or if files were edited by hand.
Engagement: you responded to every request from the AI (its questions and approval prompts), and engaged beyond approving: asking questions, pushing back, and requesting changes when a proposal did not fit your product.
Levels:

Excellent (27–30): Setup is complete. Every AI request was answered, the team engaged actively beyond approvals, and all Inception artifacts were produced through AI-DLC.
Good (23–26): Setup is complete. Every AI request was answered and the artifacts were produced through AI-DLC, but there is little engagement beyond approving what the AI proposed.
Fair (19–22): Setup has problems, some AI requests were not answered, or some artifacts were not produced through AI-DLC. A team with an incorrect setup can earn at most Fair.
Poor (0–18): AI-DLC was not set up or not used, or the record is missing or nearly empty.
D. Inception artifacts (30 points)
This criterion evaluates the files AI-DLC generates during Inception (listed in Step 4) for completeness and quality. Completeness means every expected artifact is present with real content. Quality means the content shows that your team thought it through: the requirements make sense for your product, the stories and personas are specific, and the design and units of work fit together.

Excellent (27–30): Every Inception artifact is present and of high quality. is complete and consistent with the vision; every question is answered deliberately; stories have clear acceptance criteria; personas are specific; and the execution plan, application design, and units of work (with the dependency and story-map files) fit together.requirements.md
Good (23–26): All artifacts are present and sound, with minor gaps in completeness or consistency.
Fair (19–22): All artifacts are present, but they are thin or inconsistent: some questions are answered without thought, or stories lack acceptance criteria.
Poor (0–18): Major artifacts are missing, or Inception was not completed.
E. Clarity (30 points)
This criterion checks that your and repository contain the required items. It is not about the overview paragraphs, which are graded under A, and the collaboration plan is graded on whether it is present, not on its content.README

Full (30): The lists every team member’s full name and NetID and includes the collaboration plan, and the repository is organized and easy to follow.README
Partial (10): The lists every team member’s full name and NetID and the repository is organized, but the collaboration plan is missing.README
Missing (0): Names or NetIDs are missing, or there is no usable .README
Late work follows the syllabus policy.

Midterm 
Criteria	Ratings	Points
A: LLM-integrated product proposal and its scope
view longer description

Excellent
The README provides a clear and compelling rationale for why LLMs are well-suited to the identified problem. It outlines a well-defined plan for integrating LLM capabilities into the product. The scope is ambitious enough to be a meaningful course project, rather than one minor feature, while remaining achievable by the final project deadline.
30 to >26 pts

Good
The README gives a reasonable rationale for using LLMs to address the identified problem. It describes how LLM capabilities will be integrated, although some details need further clarification. The proposed scope is generally appropriate and feasible for a course project.
26 to >22 pts

Fair
The rationale for using LLMs is limited or unclear, making it difficult to understand why LLMs are appropriate for the problem. The integration plan lacks detail. The scope may be too narrow to be a meaningful course project, or too broad to be achievable by the final project deadline.
22 to >18 pts

Poor
There is little or no justification for using LLMs, or the proposed use of LLMs is not meaningfully connected to the problem. The integration plan is missing, vague, or impractical. The scope is substantially too limited or unrealistic for the course timeline.
18 to >0 pts
/30 pts
B: AI-DLC input documents
view longer description

Excellent
Both documents are complete and cover all required sections. The content is specific, detailed, and actionable, with clear requirements, relevant technical information, and useful example code that AI-DLC can follow.
30 to >26 pts

Good
Both documents are complete and cover all required sections, but some sections are generic, vague, or not detailed enough to guide AI-DLC well.
26 to >22 pts

Fair
One or both documents are incomplete, with some required sections missing or insufficiently addressed. The content offers only partial guidance for AI-DLC.
22 to >18 pts

Poor
One or both documents are missing.
18 to >0 pts
/30 pts
C. AI-DLC process and record
view longer description

Excellent
Setup is complete. Every AI request was answered, the team engaged actively beyond approvals, and all Inception artifacts were produced through AI-DLC.
30 to >26 pts

Good
Setup is complete. Every AI request was answered and the artifacts were produced through AI-DLC, but there is little engagement beyond approving what the AI proposed.
26 to >22 pts

Fair
Setup has problems, some AI requests were not answered, or some artifacts were not produced through AI-DLC. A team with an incorrect setup can earn at most Fair.
22 to >18 pts

Poor
AI-DLC was not set up or not used, or the record is missing or nearly empty.
18 to >0 pts
/30 pts
D. Inception artifacts
view longer description

Excellent
Every Inception artifact is present and of high quality. requirements.md is complete and consistent with the vision; every question is answered deliberately; stories have clear acceptance criteria; personas are specific; and the execution plan, application design, and units of work (with the dependency and story-map files) fit together.
30 to >26 pts

Good
All artifacts are present and sound, with minor gaps in completeness or consistency.
26 to >22 pts

Fair
All artifacts are present, but they are thin or inconsistent: some questions are answered without thought, or stories lack acceptance criteria.
22 to >18 pts

Poor
Major artifacts are missing, or Inception was not completed.
18 to >0 pts
/30 pts
E. Clarity
view longer description

Full
The README lists every team member’s full name and NetID and includes the collaboration plan, and the repository is organized and easy to follow.
30 pts

Partial
The README lists every team member’s full name and NetID and the repository is organized, but the collaboration plan is missing.
10 pts

Missing
Names or NetIDs are missing, or there is no usable README.
0 pts
/30 pts
Keep in mind, this submission will count for everyone in your Class Groups group."
**AI Response**: "Drafted the README collaboration plan for four members. Included the project instruction, a shared meeting rhythm, and every milestone and final task split into four unclaimed parts: process and AI-DLC record; product definition, stories, and presentation; technical environment and local backend; profile, matching quality, and evaluation. Added name, NetID, and coding-agent placeholders for the three members not yet listed. Did not assign parts, invent names, choose a model, or approve a workflow stage. Plain Markdown validated: no diagrams and no embedded code. Updated the planning outline checkbox and aidlc-state.md."
**Context**: Requirements Analysis README work. Collaboration plan is a draft for the team to claim. Requirements Analysis is not complete, and no approval gate was advanced.

---
