# Unit of work plan

Status: Monolith/ownership/generation plan approved; unit artifacts generated and approved; milestone document review complete; stopped before Construction. Application Design is approved. Generate documentation only, then stop before Construction after final unit-artifact review.

## Proposed decomposition

The product is one local modular monolith, not twelve independently deployable services. Under the Units Generation rule's monolith convention, recommend one application unit U01, with explicit logical modules/work packages so component owners can collaborate without treating modules as separate deployments.

| Proposed module | Components | Main responsibility |
|---|---|---|
| M01 Local foundation and safeguards | C02, C10, C11, C12 | Authorized local access, secure data boundaries, audit/health, recovery. |
| M02 Profile and evidence interpretation | C03, C06 | Confirmed profile/provenance and shared bounded model/validation gateway. |
| M03 Discovery and shortlist | C04, C05, C07 | Source normalization, scan lifecycle, freshness/dedup, grounded recommendations and status. |
| M04 Reviewed bullet arrangement | C08 | Selected-job existing-bullet proposal and acceptance. |
| M05 Delivery and web composition | C09, C01 | Default in-app/opt-in email plus web routes/templates that compose all modules. |

These are planning modules, not final Python package names, team role claims or a code-generation approval. The shared C06 gateway owns extraction/explanation/arrangement protocols and is reused through typed contracts, not copied into each feature. Module dependencies follow the approved component matrix; web composition integrates modules and is not imported back by domain code. No new runtime queue, microservice, cloud resource or product scope is proposed.

## Category evaluation

| Required category | Evidence / treatment |
|---|---|
| Story grouping | Approved journey stories span profile/discovery/shortlist/delivery/bullet review and cross-cutting safeguards. Question 1 selects one unit with modules versus multiple development units. Every story gets one primary accountable module/unit and named collaborators, not ambiguous duplicate ownership. |
| Dependencies | Approved typed ports and acyclic component graph determine integration. Foundation/contracts precede feature integration; provider/clock/SMTP doubles support module tests. Question 1 confirms this approach; no new distributed communication is proposed. |
| Team alignment | README has four responsibility areas with currently blank claim cells. Question 2 controls ownership mapping without inventing names/claims. |
| Technical considerations | One local process/worker, shared SQLite boundary and secure local facilities are already approved. No differing scaling/deployment target exists by module; independent deployment question is N/A absent a scope change. |
| Business domain | Profile/evidence, opportunities, selected-job bullet review and delivery are approved capabilities. Question 1 confirms clustering while cross-cutting security/recovery remain mandatory. |
| Greenfield code organization | Question 1 chooses unit approach. Single-unit recommendation: root src/, tests/, config/, pyproject.toml and uv.lock; import package under src/app/ so the accepted app.main entry point remains possible after packaging. No application code in aidlc-docs/. Multi-unit alternative uses root src/{unit-name}/ and tests/{unit-name}/ per generation rules; import/entrypoint details must be reconciled if selected. |

## Question 1: Unit and module structure

Which decomposition should generation use? Both retain a single deployed local application and the approved typed component contracts.

A) One application unit U01 with the five logical modules above, explicit module dependencies, all 18 stories assigned, and a dependency-aware internal work-package sequence (recommended under the monolith rule).

B) Multiple development units for the five groups above, still one deployed application; explicitly document shared contracts, primary story ownership, module import boundaries and integration gates. These are not independently deployed services.

C) Other (describe exact grouping and communication boundaries after the answer tag).

[Answer]: Let's go with A, the monolith.

## Question 2: Team ownership mapping

How should the unit documents represent ownership while README role claims are still blank?

A) Map work to the existing four responsibility areas, with named individual owners left unassigned until claimed. Cross-part review and team approvals remain mandatory. Do not modify README claims.

B) Record named unit/module owners now (provide full names/NetIDs and the mapping). Preserve cross-part review; identify any agreed shared ownership precisely.

C) Other (describe after the answer tag).

[Answer]: A

## Question 3: Generation approval

Unit of work plan complete. Review the plan in aidlc-docs/inception/plans/unit-of-work-plan.md. Ready to proceed to generation? Approval applies to documentation using the choices above, not implementation.

A) Approve this plan with my answers above and generate the unit artifacts.

B) Request changes before generation (describe edits).

C) Other (describe after the answer tag).

[Answer]: A

## Planning checklist

- [x] Load approved design, requirements, stories, execution plan and enabled extension obligations.
- [x] Evaluate all required decomposition categories with explicit applicability rationale.
- [x] Propose grouping, dependency handling, ownership approach and greenfield code organization.
- [x] Present questions and explicit plan-approval prompt.
- [x] Receive all answers and analyze ambiguity/conflicts.
- [x] Resolve any ambiguity and record explicit generation-plan approval.

## Generation checklist (only after approval)

- [x] Load approved decomposition plan and identify the next unchecked generation step.
- [x] Generate application-design/unit-of-work.md with definitions, module responsibilities, component/requirement coverage, ownership, interface constraints, greenfield code organization and completion boundaries.
- [x] Generate application-design/unit-of-work-dependency.md with unit/module dependency matrix, external dependencies and integration/checkpoint order; validate no hidden cycles.
- [x] Generate application-design/unit-of-work-story-map.md assigning all 18 stories and ten FRs/nine NFRs/six MVPs, with primary accountability and supporting modules; reject gaps or unowned obligations.
- [x] Generate unit-stage extension coverage for all 40 rules, carrying security mechanism choices/recovery/PBT stage requirements into the appropriate work package.
- [x] Validate IDs, story/component coverage, dependency references, code locations and any diagrams before writing; update plan/state/audit immediately.
- [x] Present generated unit artifacts for explicit review, clearly retaining stop-before-Construction scope.
- [x] Record unit-artifact approval and mark Units Generation complete only after review.
- [x] Perform milestone consistency/completeness review and report remaining submission checks; no implementation.

## Construction handoff constraints

All units/modules inherit the approved local security uplift, RTO 4 hours/RPO 24 hours, and full PBT obligations. No unit is considered done based only on a happy-path UI. Future Functional/NFR/Infrastructure Design must resolve detailed contracts, keys/encryption, TLS/auth/audit isolation, backups/deletion retention and explicit CI/rollback/incident/test decisions. Concrete dependencies and libraries require verification before use. Units documentation may identify those gates but cannot approve deferred choices or runtime compliance.

## Extension status

All three extensions remain enabled. Unit documents and the extension matrix assign each applicable rule to an owner and downstream gate with N/A rationale. Artifact approval is recorded; no runtime compliance is claimed. Production-only cloud topology remains N/A without changing accepted local security requirements.
