# User Stories extension compliance

Scope: story coverage, not deployed compliance. Compliant means story outcomes preserve the approved obligation. Detailed architecture, implementation and test execution checks remain for their applicable stages. All extensions remain enabled.

## Security Compliance

| Rule | Status | Story coverage / N/A rationale |
|---|---|---|
| SECURITY-01 | Compliant | US-14/16; SEC-REQ-01 requires encrypted storage and TLS; exact mechanism is design work. Architecture/runtime verification is later. |
| SECURITY-02 | N/A | No load balancer, CDN or gateway intermediary. |
| SECURITY-03 | Compliant | US-17; SEC-REQ-02/NFR-08 require protected centralized structured logs. Architecture/runtime verification is later. |
| SECURITY-04 | Compliant | US-14; SEC-REQ-03 lists all required headers and local HTTPS. Architecture/runtime verification is later. |
| SECURITY-05 | Compliant | US-01/04/05/08/15; SEC-REQ-06 bounds and validates API inputs and queries. Architecture/runtime verification is later. |
| SECURITY-06 | N/A | No cloud IAM policy is created; local permissions/tool scopes are SEC-REQ-06. |
| SECURITY-07 | Compliant | US-04/14; Local network remains restricted; fixed outbound hosts and no public listener. Architecture/runtime verification is later. |
| SECURITY-08 | Compliant | US-14; SEC-REQ-04 requires authentication, ownership, CORS and session checks. Architecture/runtime verification is later. |
| SECURITY-09 | Compliant | US-15/17; SEC-REQ-07 hardening and safe errors. Architecture/runtime verification is later. |
| SECURITY-10 | Compliant | US-18; SEC-REQ-07/NFR-09 require locks/scanning/integrity; production SBOM N/A without production deployment. Architecture/runtime verification is later. |
| SECURITY-11 | Compliant | US-04/08/14/15; SEC-REQ-06/07 and NFR-06 isolate security and address malicious listing/tool misuse. Architecture/runtime verification is later. |
| SECURITY-12 | Compliant | US-14; SEC-REQ-04/05 specify credentials, sessions and conditional password/admin controls. Architecture/runtime verification is later. |
| SECURITY-13 | Compliant | US-13/18; SEC-REQ-07/08 require safe parsing and change/artifact integrity; CDN SRI conditional. Architecture/runtime verification is later. |
| SECURITY-14 | Compliant | US-17; SEC-REQ-02 requires 90-day protected logs, alerts and status view. Architecture/runtime verification is later. |
| SECURITY-15 | Compliant | US-15; SEC-REQ-08/NFR-02/03 fail closed, cleanup and safe error handler. Architecture/runtime verification is later. |
## Resiliency Compliance

| Rule | Status | Story coverage / N/A rationale |
|---|---|---|
| RESILIENCY-01 | Compliant | US-15/17/18; Prototype classification, impacts and dependency-mapping requirement recorded. Architecture/runtime verification is later. |
| RESILIENCY-02 | Compliant | US-16; User explicitly selected 4-hour RTO/24-hour RPO; no production SLA. Architecture/runtime verification is later. |
| RESILIENCY-03 | Compliant | US-18; User chose GitHub PR process plus evidence/rollback notes. Architecture/runtime verification is later. |
| RESILIENCY-04 | N/A | Implementation/deployment choices deferred to permitted NFR Design gate; no production deployment. |
| RESILIENCY-05 | Compliant | US-17; NFR-08 and reliability section require metrics/logs/status; distributed tracing N/A for single process. Architecture/runtime verification is later. |
| RESILIENCY-06 | Compliant | US-17; Health/status requirements captured; load-balancer/canary clauses N/A. Architecture/runtime verification is later. |
| RESILIENCY-07 | Compliant | US-16/17; Backup failures and capacity indicators required; cloud scaling posture N/A. Architecture/runtime verification is later. |
| RESILIENCY-08 | N/A | Production-only zone/region baseline; local non-production prototype. |
| RESILIENCY-09 | N/A | Production autoscaling/cloud capacity deployment excluded; local resource bounds remain required. |
| RESILIENCY-10 | Compliant | US-15; NFR-02/03 require timeouts, bounded resources and explicit degraded behavior. Architecture/runtime verification is later. |
| RESILIENCY-11 | Compliant | US-16; Explicit local Backup and Restore strategy and recovery validation requirements. Architecture/runtime verification is later. |
| RESILIENCY-12 | Compliant | US-16; Automated encrypted backups with restore checks required; retention selected in design; no cross-region requirement. Architecture/runtime verification is later. |
| RESILIENCY-13 | Compliant | US-16; Recovery/failback runbook and communication requirements captured. Architecture/runtime verification is later. |
| RESILIENCY-14 | N/A | Explicit test-approach decision belongs to NFR Design per rule; no resilience experiment executed here. |
| RESILIENCY-15 | N/A | Process selection permitted in NFR Design; carry forward as explicit gate. |

## PBT Compliance

| Rule | Status | Rationale |
|---|---|---|
| PBT-01 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-02 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-03 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-04 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-05 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-06 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-07 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-08 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-09 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |
| PBT-10 | N/A at story stage | Per-unit property identification/framework/test checks apply in later Functional Design, NFR Requirements, Code Generation and Build and Test. Story criteria US-02/07/09/12/18 preserve examples and invariant inputs for that work. |

## Findings

No unresolved story-level blocking finding. No cloud topology is introduced. No claim is made that examples prove model factuality, that controls exist, or that backups have passed a restore drill. Reevaluate every rule at design and Construction.
