# Requirements verification questions

Questions 1-6 are consolidated from the reviewed vision, completed technical-environment proposal, and README; their provenance is recorded beside each answer. These are existing decisions, not new approvals. Only Questions 7-10 need answers now. Do not change a previously recorded decision without noting the change.

## Question 1: Product direction

Which product and primary user should we target?

A) A student job/internship discovery assistant (recommended starting scope).

B) A networking assistant for people and events.

C) A combined career assistant with narrower features.

D) Other (describe the user, problem, and motivation).

[Answer]: A - Students and recent graduates seeking internships and entry-level jobs. Product: AI Job Application Agent. Source: reviewed vision, Product and users.

## Question 2: Core workflow

Which outcome must the MVP deliver? Add one concrete example request and expected result.

A) Discover opportunities, explain fit, and save a shortlist (recommended).

B) Compare user-supplied listings and prioritize them.

C) Discover opportunities and draft application/outreach materials for review.

D) Other (describe).

[Answer]: D - Discover recent jobs, explain fit, save/hide opportunities, and suggest an arrangement of existing confirmed resume bullets for a selected job. Example: upload two resumes, confirm extracted claims, scan, save matches, review a bullet arrangement. Source: reviewed vision MVP-01 through MVP-06. This refines the original option A and does not include invented resume text or essay generation.

## Question 3: Sources

What data access is available? Name specific sources and constraints without sharing secrets.

A) Curated dataset and user-supplied listing text for a reproducible demo.

B) One or two supported APIs/feeds with a saved demo dataset as fallback.

C) Other (describe).

[Answer]: B - Adzuna US and USAJOBS APIs, supplemented by user-pasted LinkedIn/other job text and repository fixtures. API access remains to be validated during Construction; no LinkedIn automation. Source: reviewed vision LLM and data boundaries.

## Question 4: Technical environment

Which starting point fits the team? Include experience, laptop constraints, available provider/model access, and spending limit. Exact model choice must be settled before the technical document is finalized.

A) Python local web app with a hosted LLM API.

B) Python local web app with a locally running model.

C) TypeScript local web app with a hosted LLM API.

D) Other (describe).

[Answer]: A - Proposed environment is Python 3.12, uv, FastAPI/Uvicorn/Jinja2, SQLite, Pydantic 2, HTTPX, pypdf, pytest and Ruff. Planned hosted model is OpenAI gpt-6.1-terra; the vision records Anthropic claude-haiku-5-5 as a deliberately configured fallback. Hardware/model availability and actual cost remain validation risks, not proven capabilities. Source: completed technical-environment proposal; acceptance requested in Question 10.

## Question 5: User data and success

Which data model fits the MVP? Also propose a measurable demo success target and state any required resume formats or accessibility needs.

A) One local user, manually entered profile, locally saved shortlist (recommended).

B) One local user with resume upload and saved profile/shortlist.

C) Multiple users with accounts and separate profiles.

D) Other (describe).

[Answer]: B - One local user, multiple text-bearing PDF/text resumes, pasted text, and a combined user-confirmed profile. Vision fixture checks require grounded explanations, freshness/duplicate handling, and the complete profile-to-shortlist/bullet-review journey with explicit error states. Basic keyboard-accessible labeled controls and readable errors can be specified in design; no special accessibility requirement has been stated. Source: vision and technical environment; not an invented answer about accommodations.

## Question 6: Team arrangements

Provide every member’s full name and NetID, availability before November 24, meeting frequency/format, communication channel, and initial responsibilities. Confirm or revise the proposed schedule.

A) One shared session driver with the whole team reviewing decisions.

B) One shared workflow with contributions through branches and pull requests.

C) Other (describe).

[Answer]: B - One shared AI-DLC workflow; four named members and twice-weekly online or in-person meetings, group-chat coordination, branches and cross-part PR review as recorded in README. Individual role claims and exact weekly times remain team coordination items, not inferred assignments. Source: README Collaboration plan.

## Question 7: Security Extensions

Should security extension rules be enforced for this project?

A) Yes - enforce all SECURITY rules as blocking constraints (recommended for production-grade applications).

B) No - skip all SECURITY rules (suitable for PoCs, prototypes, and experimental projects).

C) Other (describe).

[Answer]: Let's go with option A

## Question 8: Resiliency Extensions

Should the resiliency baseline be applied? It supplies directional design-time best practices from AWS reliability and resilience-review guidance across 15 practice areas, including fault tolerance, availability, observability, and recovery. It is a starting point to validate, not production certification or a guarantee of availability, RTO, or RPO; it does not replace formal review.

A) Yes - apply the baseline as directional best practices and design-time guidance.

B) No - skip it for this prototype/experimental project.

C) Other (describe).

[Answer]: A, let's apply it

## Question 9: Property-Based Testing Extension

Should property-based testing (PBT) rules be enforced?

A) Yes - all PBT rules as blocking constraints, suitable for business logic, transformations, serialization, or stateful components.

B) Partial - only pure functions and serialization round-trips.

C) No - suitable for simple CRUD, UI-only, or thin integration projects.

D) Other (describe).

[Answer]: A

## Question 10: Input baseline review

May we use the completed technical environment proposal and the synchronized README, together with the already reviewed vision, as the baseline for Requirements Analysis? Proposed stack details remain subject to real access/dependency verification during Construction. The exact model identifiers recorded in the vision have not been independently validated in this resumption.

A) Accept these input documents as the planning baseline and continue Requirements Analysis.

B) Request changes before continuing (identify the section and requested change).

C) Other (describe after the answer tag).

[Answer]: A
