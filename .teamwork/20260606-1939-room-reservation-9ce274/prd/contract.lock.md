---
template: target-template.prd.md
template_hash: 46da764df9f84c7682c82c210bb3b6f5a2294296ee5d9fb0836bcea1ddd7c1e5
template_version: "1.0"
default_min_confidence: 70
escalated: true
generated: "2026-06-07"
notes: "First derivation — no prior lock. Escalated path: Part B inherited from signed TA. 5 derived sections (exec-summary, scope-reconciliation, consolidated-risk, inherited-readiness, handoff-gate) synthesized/reconciled from inherited inputs."
---

# contract.lock.md — PRD merge template contract

This lock is the machine-readable derivation of every fillable section in
`target-template.prd.md`. The Template Validator passed the template before this
lock was generated. Any change to the template file (detected via `template_hash`
mismatch) requires a restart: new/changed section ids re-open questions in the
Strategist and surviving answers must be re-validated by the Auditor against updated
rubrics.

## Escalation context

`Escalated? = ESCALATED`. All Part B sections (`b-feasibility` through `b-adrs`) are
`Origin: inherited` from the signed Technical Assessment. The 5 derived sections
compose or reconcile from the merged inherited material. No Part B section takes the
honest-N/A path.

## Section contract table

| id | section | kind | blocks | min-confidence | inputs (derived only) | one-line rubric |
|---|---|---|---|---|---|---|
| meta | Metadata | meta | false | 0 | — | PRD ID, linked RP/TA/Intake references, escalation flag, authors, status, output language. |
| revisions | Revision History | meta | false | 0 | — | Versioned table of changes with author, date, and summary; starts at v1. |
| sign-off | Sign-off | capture | true | 85 | — | Dual sign-off row: PO confirms RP frozen (`freezeReady`); CTO confirms TA verdict (carried as-is, never re-decided). Gate is hard: no merge closes without this row resolved. |
| exec-summary | Combined Executive Summary | derived | true | 75 | a-objectives, a-scope, b-feasibility, effort-cost, success-metrics | 2–4 paragraphs: problem, what will be built, feasibility verdict, expected business outcome. Synthesized from inherited sections — invents no new facts. |
| a-objectives | A.1 Objectives and Expected Outcome | capture | true | 75 | — | Measurable outcome-based objectives carried from the frozen RP; each is an outcome (not an output). |
| a-scope | A.2 Scope (final) | capture | true | 80 | — | Final included/excluded/deferred boundaries from the frozen RP, reflecting any reconciled changes from `scope-reconciliation`. |
| a-personas | A.3 Personas / Jobs-to-be-done | capture | true | 70 | — | Who is impacted and the job each persona is hiring the product to do, inherited from the RP. |
| a-journey | A.4 User Journey (end-to-end) | capture | true | 70 | — | Happy-path end-to-end flow inherited from the RP; alternative paths and full blueprint remain in the RP source. |
| a-business-rules | A.5 Business Rules and Flows | capture | true | 70 | — | Rules, validations, and state transitions the system must enforce — summary or pointed reference to RP sections. |
| a-user-stories | A.6 User Stories + Acceptance Criteria | capture | true | 80 | — | Stories with primary Given/When/Then acceptance criteria inherited from the RP; must be testable for QA/UAT. |
| a-nfrs | A.7 Non-Functional Requirements | capture | true | 75 | — | Product NFRs from RP §8, each with how it is verified; pairs with B.4 rows on the escalated path. |
| a-edge-cases | A.8 Edge Cases and Failure Modes | capture | true | 70 | — | Edge cases and failure modes from RP §9, each with expected behavior; enables PM/Tech Lead to size unhappy paths. |
| b-feasibility | B.1 Feasibility Verdict | capture | true | 80 | — | CTO's verdict inherited from the signed TA (Feasible / Feasible with caveats); `Infeasible as scoped` never reaches this section. |
| b-nature-landscape | B.2 Nature and Technical Landscape | capture | true | 70 | — | Technical terrain inherited from the TA: current state (brownfield) or foundation/stack (greenfield). |
| b-arch-impact | B.3 Architectural Impact and Integrations | capture | true | 75 | — | Each system/area touched and nature of impact, plus required integrations, inherited from the TA. |
| b-nfr-feasibility | B.4 NFR Feasibility | capture | true | 75 | — | CTO's response to each A.7 NFR inherited from the TA; one row per A.7 NFR — loop must be closed. |
| b-alternatives | B.5 Key Alternatives Considered | capture | false | 0 | — | Technical alternatives discarded and why, inherited from the TA; prevents downstream re-litigation. |
| b-hard-constraints | B.6 Hard Constraints | capture | true | 75 | — | Non-negotiable conditions limiting the solution space, inherited from the TA; feeds `scope-reconciliation`. |
| b-adrs | B.7 ADRs (architectural level) | capture | true | 70 | — | CTO-signed architectural decisions inherited from the TA; fine-grained/implementation ADRs belong to the Tech Lead. |
| scope-reconciliation | Scope Reconciliation | derived | true | 80 | a-scope, b-feasibility, b-hard-constraints | Reconciles RP scope against TA verdict, caveats, and hard constraints; records deltas row by row; ensures `a-scope` reflects the final scope. |
| consolidated-risk | Consolidated Risk and Dependency View | derived | true | 75 | a-edge-cases, b-arch-impact, b-hard-constraints | Merges RP product/business risks (Origin: RP) with TA technical risks (Origin: TA) into one table; lists known external dependencies explicitly. |
| effort-cost | Effort and Cost (firm) | capture | true | 70 | — | Firm estimate from the TA (escalated path); labeled preliminary only on the no-escalation path. Internal use — not a client commitment. |
| inherited-readiness | Inherited Readiness and Open Dispositions | derived | true | 70 | a-scope, b-feasibility | Assumptions still to validate, Discovery unknowns (resolved/open), and delegated requirements (with owner) carried from RP/TA dispositions. |
| success-metrics | Success Criteria and Metrics (projected) | capture | true | 75 | — | Primary metrics and guardrails inherited from the RP, each with target, window, and confidence; baseline for post-rollout `metrics.md`. |
| handoff-gate | Handoff to PM — Acceptance Gate | derived | true | 80 | sign-off, scope-reconciliation, consolidated-risk, inherited-readiness | Delivery checklist the PM accepts or rejects; every box must be checkable from the merged document; asserts merge is complete — invents nothing. |

## Blocking sections

Sections with `blocks=true` that carry `min-confidence` at or above the default
threshold (70) must each reach their stated confidence before the document can be
frozen (`handoffReady`). The hard gate is `sign-off` at 85 — no merge closes without
dual sign-off resolved. Other blocking sections and their thresholds:

| id | min-confidence | gate role |
|---|---|---|
| sign-off | 85 | Hard gate — dual sign-off required |
| a-scope | 80 | Scope must be final (reconciled) before handoff |
| a-user-stories | 80 | Stories must be testable for QA/UAT acceptance |
| b-feasibility | 80 | Verdict carried from TA; must be explicitly confirmed inherited |
| scope-reconciliation | 80 | Reconciliation work must be complete |
| handoff-gate | 80 | Delivery checklist must be fully resolvable |
| exec-summary | 75 | Synthesized view must be accurate to inherited inputs |
| a-objectives | 75 | Outcomes must be measurable and carried faithfully |
| a-nfrs | 75 | NFRs must pair with B.4 rows (A.7↔B.4 invariant) |
| b-arch-impact | 75 | Architectural impact must be complete for risk consolidation |
| b-nfr-feasibility | 75 | Every A.7 NFR must have a feasibility answer |
| b-hard-constraints | 75 | Constraints feed scope-reconciliation; must be resolved |
| consolidated-risk | 75 | Merged risk view must be complete before handoff |
| success-metrics | 75 | Metrics must be explicit for post-rollout comparison |
| a-personas | 70 | (default threshold) |
| a-journey | 70 | (default threshold) |
| a-business-rules | 70 | (default threshold) |
| a-edge-cases | 70 | (default threshold) |
| b-nature-landscape | 70 | (default threshold) |
| b-adrs | 70 | (default threshold) |
| effort-cost | 70 | (default threshold) |
| inherited-readiness | 70 | (default threshold) |

## Non-blocking sections

Sections with `blocks=false` do not gate freeze. They are filled for completeness
and human review but a low or absent confidence value does not halt the pipeline:

| id | min-confidence | note |
|---|---|---|
| meta | 0 | Filled from works index — reference fields, not confidence-rated |
| revisions | 0 | Filled from audit trail — administrative record |
| b-alternatives | 0 | Informational only — "—" with `Disposition: decided` if none |

## Derived section inputs (escalated path)

| id | kind | inputs required before synthesis |
|---|---|---|
| exec-summary | derived | a-objectives, a-scope, b-feasibility, effort-cost, success-metrics |
| scope-reconciliation | derived | a-scope, b-feasibility, b-hard-constraints |
| consolidated-risk | derived | a-edge-cases, b-arch-impact, b-hard-constraints |
| inherited-readiness | derived | a-scope, b-feasibility |
| handoff-gate | derived | sign-off, scope-reconciliation, consolidated-risk, inherited-readiness |

## Consistency invariants (Auditor enforces)

1. **A.7 ↔ B.4**: every NFR row in `a-nfrs` must have a matching feasibility row in
   `b-nfr-feasibility`. A declared NFR with no answer is a gap, not a detail.
2. **A.2 ↔ scope-reconciliation**: if `scope-reconciliation` recorded any change
   (Re-scoped / Removed / Added), `a-scope` must reflect the reconciled boundaries,
   not the pre-TA scope. The two sections must agree.

A flagged inconsistency routes to the Reconciler — it is never silently resolved.

<!-- END OF DOCUMENT -->
