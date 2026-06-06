---
template: target-template.origination-record.md
template_hash: 6d91450cbf11f615699612c7b47c8c7f6876ba4ce0a85a721196182479f9fe4f
template_version: v1
default_min_confidence: 70
generated: 2026-06-06
---

# Contract

| id | section | kind | blocks | min-confidence | inputs | condition | rubric (one line) |
|----|---------|------|--------|----------------|--------|-----------|-------------------|
| meta | Metadata | meta | false | 0 | — | — | Record ID, version, originator, dates, status, output language |
| revisions | Revision history | meta | false | 0 | — | — | Version table: date, event, brief summary of change |
| readiness | Readiness received | derived | false | 0 | problem,reach,impact,originator,urgency | — | Computed readiness score + gate status from captured sections |
| problem | Problem (the pain, not the solution) | capture | true | 80 | — | — | Pain with observable symptoms — what hurts, for whom, how it shows up; NOT a solution |
| originator | Originator & context | capture | true | 70 | — | — | Who raised it and in what situation, plus the channel it came through |
| reach | Who is impacted (reach) | capture | true | 70 | — | — | Personas/segments/teams who feel the pain, each with how they are affected |
| impact | Business impact | capture | true | 70 | — | — | Value across revenue/retention/operational/competitive/compliance — quantified when possible |
| urgency | Urgency — why now | capture | false | 70 | — | — | Why now and cost of waiting — a window, deadline, or compounding cost |
| priority | Declared priority | capture | false | 0 | — | — | Submitter's priority level AND the reason behind it (not just the label) |
| nature-signal | Nature signal — new vs. existing software | capture | false | 0 | — | — | Lightweight greenfield/brownfield signal seeding PO classification — New capability / Existing software / Not sure |
| triage | Triage — routing decision | derived | false | 0 | problem,reach,impact,urgency,assumptions | — | AI-draft routing decision (criteria table + Decision/Rationale); flagged for human sign-off |
| cto_escalation | Architectural escalation | derived | false | 0 | impact,constraints,assumptions | — | Whether CTO/architectural review is needed before scope can freeze, with one-line reason |
| assumptions | Assumptions | capture | false | 0 | — | — | Conditions assumed true at capture, each with draft verdict and who validates |
| constraints | Constraints | capture | false | 70 | — | — | Conditions limiting solution space, typed (Time/Budget/Legal/Technical/Scope/External) |
| discovery | Discovery brief | derived | false | 0 | triage | triage.decision==Discovery | Unknowns table + time-box; fill ONLY when triage decision is Discovery |
| handoff | Handoff | derived | false | 0 | triage | — | Routing destination bullets derived from confirmed triage decision |

## Notes

- Fresh run — no prior contract.lock.md existed; no restart required.
- **Gate sections** (blocks=true): `problem` (min-confidence=80), `originator`, `reach`, `impact` (all min-confidence=70). These four must reach their threshold or carry an honest disposition (assumption/discovery/deferred) before the pipeline gate clears.
- `urgency` and `constraints` have min-confidence=70 but blocks=false — they are graded but do not hard-block the gate.
- `discovery` is conditional on `triage.decision==Discovery`; include in the document only when that condition holds.
- All derived sections (`readiness`, `triage`, `cto_escalation`, `discovery`, `handoff`) are recomputed from their listed inputs and do not carry their own Provenance blocks; `triage` signals confidence via the DRAFT banner and `low_confidence` disposition.

<!-- END OF DOCUMENT -->
