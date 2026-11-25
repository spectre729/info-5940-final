# Unit of work story and requirement map

Status: Generated under approved U01/five-module plan; approved in chat; see audit.md. Every story has exactly one primary module accountable for its observable outcome and explicit collaborators. All belong to U01; contributors are not additional deployment units. Individual ownership remains unassigned; README role areas guide collaboration without changing claim cells.

## Story ownership

| Story | Title | Unit | Primary module | Supporting modules |
|---|---|---|---|---|
| US-01 | Import my background | U01 | M02 | M05,M01 |
| US-02 | Confirm and correct my profile | U01 | M02 | M01,M05 |
| US-03 | Update my confirmed background | U01 | M02 | M03,M01,M05 |
| US-04 | Retrieve supported opportunities | U01 | M03 | M02,M01 |
| US-05 | Review a job I paste | U01 | M03 | M05,M01 |
| US-06 | Refresh on demand or schedule | U01 | M03 | M05,M01 |
| US-07 | Understand listing freshness | U01 | M03 | M05 |
| US-08 | Understand fit and gaps | U01 | M03 | M02,M05 |
| US-09 | Save or hide without repeat recommendations | U01 | M03 | M01,M05 |
| US-10 | Read results in the app | U01 | M05 | M03 |
| US-11 | Opt into email delivery | U01 | M05 | M01,M03 |
| US-12 | Review existing resume bullets for one job | U01 | M04 | M02,M03,M01,M05 |
| US-13 | Inspect and remove personal data | U01 | M01 | M02,M03,M05 |
| US-14 | Protect my local session and stored data | U01 | M01 | M05 |
| US-15 | Keep useful results when a dependency fails | U01 | M03 | M01,M02,M05 |
| US-16 | Restore saved work after local failure | U01 | M01 | M02,M03,M05 |
| US-17 | Know whether a scan or backup needs attention | U01 | M01 | M05 |
| US-18 | Review a reproducible local demonstration | U01 | M05 | M01,M02,M03,M04 |

## Requirement ownership

| Requirement | Unit | Primary module | Supporting modules |
|---|---|---|---|
| FR-01 | U01 | M02 | M01,M05 |
| FR-02 | U01 | M02 | M01,M03 |
| FR-03 | U01 | M03 | M01,M05 |
| FR-04 | U01 | M03 | M01,M05 |
| FR-05 | U01 | M03 | M05 |
| FR-06 | U01 | M03 | M02,M05 |
| FR-07 | U01 | M03 | M01,M05 |
| FR-08 | U01 | M05 | M01,M03 |
| FR-09 | U01 | M04 | M01,M02,M03,M05 |
| FR-10 | U01 | M01 | M02,M03,M05 |
| NFR-01 | U01 | M01 | M05 |
| NFR-02 | U01 | M01 | M02,M03,M05 |
| NFR-03 | U01 | M03 | M01,M02,M05 |
| NFR-04 | U01 | M01 | M02,M03,M05 |
| NFR-05 | U01 | M05 | M01,M02,M03,M04 |
| NFR-06 | U01 | M01 | M02,M03,M04,M05 |
| NFR-07 | U01 | M01 | M02,M03,M04,M05 |
| NFR-08 | U01 | M01 | M02,M03,M04,M05 |
| NFR-09 | U01 | M01 | M02,M03,M04,M05 |
| MVP-01 | U01 | M02 | M01,M05 |
| MVP-02 | U01 | M03 | M01,M02,M05 |
| MVP-03 | U01 | M03 | M02,M05 |
| MVP-04 | U01 | M03 | M01,M05 |
| MVP-05 | U01 | M05 | M01,M03 |
| MVP-06 | U01 | M04 | M01,M02,M03,M05 |

## Component ownership

| Component | Unit | Primary module |
|---|---|---|
| C02 | U01 | M01 |
| C10 | U01 | M01 |
| C11 | U01 | M01 |
| C12 | U01 | M01 |
| C03 | U01 | M02 |
| C06 | U01 | M02 |
| C04 | U01 | M03 |
| C05 | U01 | M03 |
| C07 | U01 | M03 |
| C08 | U01 | M04 |
| C09 | U01 | M05 |
| C01 | U01 | M05 |

## Completeness and acceptance

18 of 18 stories, 10 of 10 FRs, 9 of 9 NFRs, 6 of 6 MVPs and 12 of 12 components have one primary owner. Supporting participation does not transfer accountability. US-18 is M05-led integration with all modules and the whole team's evidence review; dependency scanning/PBT framework/CI remain cross-cutting M01 coordination with each module responsible for its own tests. Part 1 coordinates records/submission; Part 2 validates requirements/story/demo narrative; Part 3 technical backend/foundation/delivery; Part 4 profile/matching/evaluation/UI. This does not claim an individual has accepted any part.

No exclusion has become an assigned stretch feature. Do not mark a story implemented during Inception. Construction must link code/tests to these IDs and preserve example plus generated/integration evidence. Security/recovery work is owned, not left as optional post-demo cleanup. Unit artifacts await review; no Construction approval follows automatically.
