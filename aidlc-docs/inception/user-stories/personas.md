# User personas

Status: Generated under approved story plan; approved in chat; see audit.md. These are synthetic design archetypes, not research findings, real people, or separate authorization roles. One local user uses each installation.

## P-01: Student seeking internships

- Context: A current student with coursework, projects and possibly limited professional experience spread across multiple resumes.
- Goal: Find recent internships that fit actual skills and stated education/eligibility preferences, without repeatedly screening broad results.
- Friction: Project experience may use different wording from listings; requirements and dates may be incomplete; model extraction can misread a resume.
- Needs: Correct extracted claims, retain evidence, see gaps and unknowns, compare a pasted role, and avoid repeated listings.
- Journey: Import -> review/correct claims -> discover/paste opportunities -> inspect freshness/fit -> save/hide -> optionally review existing bullets -> control delivery and retained data.
- Constraints: Local laptop app, finite attention and optional hosted-provider access. No assumed location, citizenship, work arrangement or budget. No application submission or automatic outreach.
- Representative scenario: Import two resumes, reject one mis-extracted claim, scan fixtures and a configured source, save a grounded match and reject an unsuitable bullet arrangement.
- Relevant stories: US-01, US-02, US-03, US-04, US-05, US-06, US-07, US-08, US-09, US-10, US-11, US-12, US-13, US-14, US-15, US-16, US-17, US-18.

## P-02: Recent graduate seeking entry-level roles

- Context: A recent graduate with several resume versions emphasizing different experiences, seeking entry-level roles.
- Goal: Receive a small useful shortlist with enough evidence to decide where to apply.
- Friction: Manual searches repeat work; old/unclear postings and duplicates distract; silently merged resume facts could misrepresent qualifications.
- Needs: A canonical confirmed profile, recurring scans while the app runs, persisted shortlist decisions, clear explanations, opt-in email and recovery of saved work.
- Journey: Confirm combined background -> scheduled/manual discovery -> review gaps and source evidence -> save/hide -> accept an arrangement of confirmed bullets for one job -> resume after restart.
- Constraints: One local user, scans/email stop when the app closes, source API and model access must be validated. No assumed personal preferences from the reference system.
- Representative scenario: Confirm a profile, enable email, save two roles, reopen the app after a gap, see one catch-up scan and retain saved roles without duplicate new recommendations.
- Relevant stories: US-01, US-02, US-03, US-04, US-05, US-06, US-07, US-08, US-09, US-10, US-11, US-12, US-13, US-14, US-15, US-16, US-17, US-18.

## Shared responsibilities and differences

P-01 emphasizes validating project/course experience and internship eligibility; P-02 emphasizes combining resume variants and recurring entry-level discovery. Both need the same privacy, security, recovery and transparent-failure outcomes. Supporting review/demo stories describe what either user can inspect; they do not invent a separate administrator or automatic application workflow. Security and backup mechanisms remain design decisions.
