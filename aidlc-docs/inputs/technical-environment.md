# Technical environment

Status: Template - incomplete and not team-approved.

Replace every `TODO` with an explicit choice and version where relevant. Use "Not applicable" with a reason when appropriate. Examples below illustrate documentation structure; they do not select Python or an API framework for the project. Adapt them to the chosen stack before approval.

## Language, package manager, and framework

| Area | Choice and version | Reason |
|---|---|---|
| Language/runtime | TODO | TODO |
| Package manager and lockfile | TODO | TODO |
| UI framework | TODO | TODO |
| API/backend framework | TODO | TODO |
| Validation/schema library | TODO | TODO |
| Persistence | TODO | TODO |
| Test framework | TODO | TODO |
| Formatting/linting | TODO | TODO |

- Supported operating systems and minimum hardware: TODO
- Coding agents used by the team: TODO
- Required methodology: AI-DLC v1.0.1; installed release verification: TODO

## Cloud provider and deployment model

The assignment permits a local-only product; cloud hosting is not required.

- Selected deployment model: TODO
- Cloud provider, or "None - runs locally": TODO
- Local components and how they communicate: TODO
- Installation command: TODO
- Development/start command: TODO
- Test command: TODO
- Local URL/port and persistent data location: TODO
- Offline/demo fallback and seed data: TODO

## LLM integration

| Setting | Decision |
|---|---|
| Provider and exact planned model | TODO |
| Hosted API or local inference | TODO |
| SDK/API interface and version | TODO |
| Required configuration variable names | TODO |
| Per-run/token budget and timeout | TODO |
| Structured-output validation | TODO |
| Retry/error behavior | TODO |
| Test double and repeatable fixtures | TODO |

- Agent tools and their input/output contracts: TODO
- Data sent to the model and provider retention considerations: TODO
- Model availability/hardware validation plan: TODO

## Data sources and storage

| Source or data type | Access method/format | Storage and retention | Constraints |
|---|---|---|---|
| Opportunity listings | TODO | TODO | TODO |
| User profile | TODO | TODO | TODO |
| Saved shortlist | TODO | TODO | TODO |

- Deduplication key and provenance fields: TODO
- Supported input formats, size limits, and validation: TODO
- External API credentials, rate limits, and demo fixtures: TODO

## Prohibited libraries

Document deliberate project constraints, not arbitrary bans. If none are prohibited, state that explicitly with rationale instead of leaving placeholder rows.

| Prohibited library or category | Reason | Approved alternative |
|---|---|---|
| TODO | TODO | TODO |

## Security basics

- Secret storage and ignored local configuration files: TODO
- Personal data minimization, deletion, and retention: TODO
- Input validation and safe display of retrieved content: TODO
- Treatment of external text as untrusted model input: TODO
- Tool permissions and safeguards for any external actions: TODO
- Authentication and local network exposure decision: TODO
- Logging/redaction policy: TODO
- Dependency/version management: TODO

These basics are required input content independently of whether the optional Security Baseline extension is enabled. Extension opt-ins remain in the requirements question file.

## Example endpoint

Illustrative contract only; replace fields and paths to match the approved product and framework. Add a concrete route implementation in the selected language/framework before final team review.

- Method/path: `POST /api/opportunities/search`
- Purpose: find sourced opportunities for a supplied profile.
- Example request:

```json
{"skills": ["Python"], "target_role": "software internship", "limit": 5}
```

- Example successful response:

```json
{"opportunities": [{"id": "demo-001", "title": "Example internship", "source_url": "https://example.com/jobs/demo-001", "fit_explanation": "The supplied listing mentions Python."}]}
```

The URL and listing are fictional fixture data, not a real recommendation.

- Request validation and error response examples: TODO
- Timeout/provider-failure behavior: TODO
- Endpoint implementation in selected framework: TODO

## Example function

Illustrative pure Python function for matching normalized skills; this is not an approved ranking algorithm. Replace or adapt it and specify the real function contract after stack selection.

```python
def matching_skills(profile_skills: list[str], required_skills: list[str]) -> list[str]:
    """Return sorted, case-insensitive skill overlap without duplicates."""
    profile = {skill.strip().casefold() for skill in profile_skills if skill.strip()}
    required = {skill.strip().casefold() for skill in required_skills if skill.strip()}
    return sorted(profile & required)
```

- Selected function, module location, and business purpose: TODO
- Input/output contract and edge cases: TODO

## Example test

Illustrative Python assertion, assuming the function above is available. Adapt imports and assertions to the chosen test framework.

```python
def test_matching_skills_normalizes_and_deduplicates():
    actual = matching_skills([" Python ", "PYTHON", "SQL"], ["python", "Go", ""])
    assert actual == ["python"]
```

## Test and evaluation approach

- Unit tests for deterministic logic: TODO
- Integration tests for retrieval, persistence, and model boundary: TODO
- End-to-end local demo scenario: TODO
- LLM relevance/factuality evaluation fixtures and targets: TODO
- Error-path tests, including unavailable sources/model: TODO
- Which tests use mocks versus live services and their cost: TODO

## Team review

- [ ] All placeholders replaced; versions and commands are specific.
- [ ] Prohibited-libraries table contains decisions and reasons, or explicit justified N/A.
- [ ] Endpoint, function, and test examples adapted to the chosen stack.
- [ ] Examples parse and agree with the documented contracts.
- [ ] Local setup and model access are feasible on team laptops.
- [ ] Consistent with vision, README, and requirements answers.
- [ ] Reviewed by the whole team.
- Reviewers and review date: TODO
- Approval reference in audit.md: TODO
