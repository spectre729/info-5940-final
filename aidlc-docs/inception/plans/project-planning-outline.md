# Proposed project plan

Status: Draft for team discussion; not an approved execution plan.

## Assignment requirements

Source: project-description.pdf, pages 1-2 and 5-7.
- November 24, 2026, 11:59 PM: Inception milestone repository submission.
- December 16, 2026: final project, including Construction, demo video, recorded presentation, repository, and peer evaluation.
- AI-DLC v1.0.1 is required; installed version still needs verification.
- Local execution is sufficient; Operations is not required.

## Proposed product

The README suggests discovering jobs, internships, and networking opportunities. Recommended starting scope: a student career opportunity assistant.

Core journey: enter skills and preferences; search a small supported set of sources; review relevant opportunities with source links and evidence-based fit explanations; save a shortlist and next steps.

The LLM interprets preferences, chooses supported search tools, and explains matches. Ordinary code handles storage, filtering, and deduplication. Missing source facts remain unknown. Networking discovery, application drafting, and resume uploads require explicit scope decisions. Automatic applications and outreach are proposed out of scope.

## Proposed schedule and workflow

1. November 19-20: Team problem discussion and scope decisions; prepare and team-review README, vision, and technical environment documents.
2. November 20-21: Requirements Analysis and User Stories, with answers and approvals.
3. November 21-23: Workflow Planning, Application Design, and Units Generation, with approvals.
4. November 24: Verify rubric coverage, artifact consistency, complete audit/state records, and public repository accessibility; submit.
5. November 25-December 6: Proposed Construction window, one approved unit at a time.
6. December 7-12: Integration, evaluation, and demo preparation.
7. December 13-16: Final fixes, recordings, presentation, and submission buffer.

Dates other than assignment deadlines are proposed working targets. Team availability is unknown.

Reverse Engineering is skipped because there is no application code. User Stories, Application Design, and Units Generation are included because the assignment requires them. Stop after approved Units Generation for the milestone; Construction is later work.

## Deliverables

README: full names and NetIDs, coding agents and AI-DLC version, problem and LLM rationale, integration plan and planned model/provider, feasible scope, and collaboration plan.

Vision: product and users, MVP scope, explicit exclusions, and open questions.

Technical environment: language/version, package manager, framework, local execution model, test framework, prohibited libraries with reasons and alternatives, security basics, and example endpoint, function, and test. Exact technologies remain undecided.

Inception: requirements and answered questions; stories and personas; execution plan; application design; units, dependencies, and story map. Maintain audit.md and aidlc-state.md throughout.

## Progress

- [x] Inspect workspace: greenfield, README outline, assignment PDF, and workflow rules; no application code or build system.
- [x] Read assignment and identify deliverables and deadlines.
- [x] Propose product direction and schedule.
- [x] Prepare questions, including extension opt-ins.
- [ ] Receive and validate team answers.
- [x] Create vision and technical environment fill-in templates.
- [x] Draft README part 1 using user answers and existing-system reference.
- [x] Draft README planned LLM integration and project scope/feasibility sections.
- [ ] Fill and review README, vision, and technical environment inputs.
- [ ] Complete and approve requirements.
- [ ] Complete and approve stories/personas.
- [ ] Complete and approve formal execution plan.
- [ ] Complete and approve application design and units.
- [ ] Verify milestone deliverables and stop before Construction.

## Evaluation to refine

Use fixed student profiles and opportunity data to evaluate relevance, factual grounding, and completion of the discovery-to-shortlist journey. Agree on measurable targets before implementation. Handle unavailable sources and model failures explicitly.

## Extension compliance

Security, resiliency, and property-based testing opt-ins are pending. Full rules remain deferred; no Requirements Analysis completion is claimed.
