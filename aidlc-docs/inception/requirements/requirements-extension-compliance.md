# Requirements Analysis extension compliance

Scope: requirement coverage only. No application code, deployment, dependency configuration, or security verification exists yet. N/A stage-specific items must be reevaluated downstream. This is not certification or production readiness.

## Security Compliance

| Rule | Status | Rationale/evidence |
|---|---|---|
| SECURITY-01 | Compliant | SEC-REQ-01 requires encrypted storage and TLS; exact mechanism is design work. |
| SECURITY-02 | N/A | No load balancer, CDN or gateway intermediary. |
| SECURITY-03 | Compliant | SEC-REQ-02/NFR-08 require protected centralized structured logs. |
| SECURITY-04 | Compliant | SEC-REQ-03 lists all required headers and local HTTPS. |
| SECURITY-05 | Compliant | SEC-REQ-06 bounds and validates API inputs and queries. |
| SECURITY-06 | N/A | No cloud IAM policy is created; local permissions/tool scopes are SEC-REQ-06. |
| SECURITY-07 | Compliant | Local network remains restricted; fixed outbound hosts and no public listener. |
| SECURITY-08 | Compliant | SEC-REQ-04 requires authentication, ownership, CORS and session checks. |
| SECURITY-09 | Compliant | SEC-REQ-07 hardening and safe errors. |
| SECURITY-10 | Compliant | SEC-REQ-07/NFR-09 require locks/scanning/integrity; production SBOM N/A without production deployment. |
| SECURITY-11 | Compliant | SEC-REQ-06/07 and NFR-06 isolate security and address malicious listing/tool misuse. |
| SECURITY-12 | Compliant | SEC-REQ-04/05 specify credentials, sessions and conditional password/admin controls. |
| SECURITY-13 | Compliant | SEC-REQ-07/08 require safe parsing and change/artifact integrity; CDN SRI conditional. |
| SECURITY-14 | Compliant | SEC-REQ-02 requires 90-day protected logs, alerts and status view. |
| SECURITY-15 | Compliant | SEC-REQ-08/NFR-02/03 fail closed, cleanup and safe error handler. |
## Resiliency Compliance

| Rule | Status | Rationale/evidence |
|---|---|---|
| RESILIENCY-01 | Compliant | Prototype classification, impacts and dependency-mapping requirement recorded. |
| RESILIENCY-02 | Compliant | User explicitly selected 4-hour RTO/24-hour RPO; no production SLA. |
| RESILIENCY-03 | Compliant | User chose GitHub PR process plus evidence/rollback notes. |
| RESILIENCY-04 | N/A | Implementation/deployment choices deferred to permitted NFR Design gate; no production deployment. |
| RESILIENCY-05 | Compliant | NFR-08 and reliability section require metrics/logs/status; distributed tracing N/A for single process. |
| RESILIENCY-06 | Compliant | Health/status requirements captured; load-balancer/canary clauses N/A. |
| RESILIENCY-07 | Compliant | Backup failures and capacity indicators required; cloud scaling posture N/A. |
| RESILIENCY-08 | N/A | Production-only zone/region baseline; local non-production prototype. |
| RESILIENCY-09 | N/A | Production autoscaling/cloud capacity deployment excluded; local resource bounds remain required. |
| RESILIENCY-10 | Compliant | NFR-02/03 require timeouts, bounded resources and explicit degraded behavior. |
| RESILIENCY-11 | Compliant | Explicit local Backup and Restore strategy and recovery validation requirements. |
| RESILIENCY-12 | Compliant | Automated encrypted backups with restore checks required; retention selected in design; no cross-region requirement. |
| RESILIENCY-13 | Compliant | Recovery/failback runbook and communication requirements captured. |
| RESILIENCY-14 | N/A | Explicit test-approach decision belongs to NFR Design per rule; no resilience experiment executed here. |
| RESILIENCY-15 | N/A | Process selection permitted in NFR Design; carry forward as explicit gate. |

## PBT Compliance

| Rule | Status | Rationale/evidence |
|---|---|---|
| PBT-01 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-02 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-03 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-04 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-05 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-06 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-07 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-08 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-09 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |
| PBT-10 | N/A at this stage | Requirements carry the full property/testing obligations; rule verification applies at Functional Design, NFR Requirements, Code Generation or Build and Test, not Requirements Analysis. Reevaluate then. |

## Findings

No unresolved requirement-level findings. Earlier security gaps are resolved at requirements level by SEC-REQ-01 through SEC-REQ-08, not by pretending the prototype already implements them. Mechanism selection and verification remain downstream gates. No N/A designation disables an enabled extension.
