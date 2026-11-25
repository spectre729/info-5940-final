# Enabled extension follow-up questions

Questions 7-10 in requirement-verification-questions.md are all answered A. Security, resiliency, and full property-based testing are enabled, and the input baseline is accepted. These follow-ups come from the newly loaded rules, rather than missing original answers. Full extension enablement does not require adding cloud hosting: production-only cloud topology requirements are not applicable to this local course prototype.

## Question 1: Security baseline and local scope

The enabled Security Baseline requires encryption at rest/in transit (SECURITY-01), centralized structured logs (SECURITY-03), web security headers (SECURITY-04), authenticated resource access (SECURITY-08), secure credentials/sessions (SECURITY-12), and protected audit logs/alerting (SECURITY-14). The current plain local SQLite/files and HTTP start command do not specify those controls. We cannot declare these applicable controls satisfied simply because the app is local. This needs a documented design update; no production infrastructure is automatically authorized.

A) Keep Security Baseline enabled and incorporate its applicable controls into the local design. Maintain a single local user; define encrypted storage/transport, local access protection, and secure logging in design. No cloud hosting or multiple-user account system is requested.

B) Revise Question 7 to disable the optional full Security Baseline for this prototype, while retaining the technical environment's existing security basics.

C) Other (describe the intended decision and constraints after the answer tag).

[Answer]: A

## Question 2: Recovery goals and disaster recovery strategy

RESILIENCY-02 requires an explicit recovery decision before requirements are finalized. Recovery time (RTO) is how long restoration may take; recovery point (RPO) is how much recent saved data may be lost. The following are local-prototype interpretations of the rule's Backup and Restore choice; no cloud zones or regions are needed. Targets apply while using the app and reflect loss of local files, not continuous service while the app is closed.

A) Local Backup and Restore: target recovery within 4 hours, at most 24 hours of saved profile/shortlist changes lost. Plan encrypted automated backups and a tested restore procedure; define retention during design.

B) Local Backup and Restore with different targets: specify RTO, RPO and the importance of preserving personal data.

C) Other (describe a justified alternative, including any deliberate demo-data-only recovery policy).

[Answer]: A

## Question 3: Change management

RESILIENCY-03 requires the team's choice of process before finalizing requirements. README already records branches, cross-part PR review, and shared AI-DLC approvals.

A) Use that existing GitHub branch/PR review process as change management, adding test evidence and a rollback note to changes affecting stored data or local runtime behavior.

B) Have AI-DLC propose a separate lightweight change record, approval, and rollback process for team review.

C) Other (describe the existing process or a justified exemption).

[Answer]:A

## Deferred design decisions

CI tooling, rollback and deployment details (RESILIENCY-04), incident response (RESILIENCY-15), and resiliency test planning (RESILIENCY-14) will be asked at their permitted design stages. Cloud multi-zone topology and autoscaling rules apply to production deployments, which this course MVP does not include. Full PBT requires domain properties, stateful tests and reproducible generated inputs alongside examples; no live LLM calls are needed in generated tests. A Python PBT framework will be selected in NFR Requirements, with dependency configuration during Construction.
