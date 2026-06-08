---
template: target-template.technical-assessment.md
template_hash: b9590cf5ac7a27f9b05cde23643ec98f1f88df1134dc9721281a7d6b65a6da23
template_version: v1
default_min_confidence: 70
generated: 2026-06-07
notes: >
  First derivation — no prior lock existed. Two-paths-one-template construct:
  `tech-classification` (id) governs which path is in force. Brownfield/Hybrid
  activates `current-state`; Greenfield/Hybrid activates `tech-foundation`.
  The non-applicable path clears via an honest `Disposition: decided` N/A entry
  and is NOT a gate failure.
---

# Contract

<!-- Blocking gate: a section with blocks=true must reach its min-confidence
     threshold OR carry an honest disposition (assumption / discovery / deferred /
     decided-N/A) before the assessment can be signed off. -->

| id | section | kind | blocks | min-confidence | rubric (one line) |
|----|---------|------|--------|----------------|-------------------|
| meta | Metadata | meta | false | 0 | Stable IDs (TA-YYYY-NNN, linked RP, Intake), owner, status, feasibility mirror, sign-off date, output language |
| revisions | Revision History | meta | false | 0 | Version table: version, date, author, status, change summary |
| feasibility-verdict | Feasibility Verdict | capture | true | 85 | CTO's first-class judgment: verdict + defensible rationale + terrain (KB anchor or "undocumented → Discovery") + caveats (if applicable) + generates |
| tech-classification | Technical classification and Knowledge Base | capture | true | 80 | Governs the document: confirmed demand nature (Greenfield / Brownfield / Hybrid), path to fill, KB status (Exists / Partial / Does not exist) with reference |
| po-questions | PO Questions Addressed | capture | true | 70 | Each technical unknown the PO escalated with its CTO answer; or explicit "no specific question was escalated" |
| current-state | BROWNFIELD Path — Current state / Technical landscape | capture | true | 75 | [BROWNFIELD/HYBRID only] Existing patterns/conventions, integration points with coupling + risk, technical debt + regression risk + test coverage; N/A-greenfield clears via Disposition: decided |
| tech-foundation | GREENFIELD Path — Technical foundation | capture | true | 75 | [GREENFIELD/HYBRID only] Stack selection with criteria per layer + discarded alternatives, target architecture (C4 context/container), structure/repo conventions; N/A-brownfield clears via Disposition: decided |
| affected-systems | Affected Systems and Components | capture | true | 70 | Every service/module touched and nature of impact (new / modified / consumed only); inherited from RP scope |
| architectural-impact | Architectural Impact | capture | true | 75 | Per-area impact + architectural note (pattern to follow/avoid) for each relevant area: data model, events, frontend, security, multi-tenancy, performance, observability |
| integrations | Required Integrations | capture | true | 70 | Each required integration: type, protocol, feasibility/known risks; "none" with Disposition: decided if none |
| build-vs-buy | Build vs. Buy | capture | false | 0 | Per non-trivial capability: Build/Buy/Reuse, rationale, effect on cost/timeline; skip with Disposition: decided if no make-or-buy decision |
| alternatives | Alternatives Considered | capture | true | 70 | One row per significant alternative: pros, cons, and explicit why-not-chosen; rationale, not just the conclusion |
| nfr-feasibility | NFR Feasibility | capture | true | 75 | Per NFR inherited from RP §8: feasible? (Yes / With caveats / No), how achieved, risk/caveat; infeasible NFR is a veto/re-scoping signal |
| testability-observability | Testability and Observability | capture | true | 70 | Test strategy + test data/environment covering RP §9 edge cases; telemetry/technical metrics + logs/alerts for production visibility |
| hard-constraints | Hard Constraints | capture | true | 75 | Non-negotiable conditions: type, detail, effect on scope; "none" with Disposition: decided if none |
| tech-risks | Technical Risks and Mitigations | capture | true | 75 | Technical risks only (category, probability, impact, mitigation); product/business risks stay in the RP |
| adrs | Architecture Decisions (ADRs) | capture | true | 75 | CTO-level architectural decisions: decision + rationale + CTO sign-off; engine proposes from KB, CTO approves/adjusts |
| effort-cost | Effort and Cost Assessment (firm) | capture | true | 70 | CTO's firm estimates: dev effort by area + seniority, infra impact, third-party cost, recurring operational cost, TCO assessment |
| discovery-path | Discovery Path | capture | false | 0 | Fill only if a technical unknown blocks completion: spike/investigation + who + suggested time-box; "—" with Disposition: decided if nothing blocks |

---

## Two-Paths Gate Logic

`tech-classification` is the **governing section**. Its resolved value determines
which path entries are in-force blocking gates and which clear via N/A disposition:

| tech-classification result | `current-state` gate | `tech-foundation` gate |
|---------------------------|----------------------|------------------------|
| Greenfield | N/A — clears via `Disposition: decided` | **Blocking** (min-conf 75) |
| Brownfield | **Blocking** (min-conf 75) | N/A — clears via `Disposition: decided` |
| Hybrid | **Blocking** (min-conf 75) | **Blocking** (min-conf 75) |

A `Disposition: decided` N/A entry on the non-applicable path is an **honest
disposition** that satisfies the gate — it is not a gap.

---

## Gate Summary

- **Sections contracted:** 19
- **Blocking sections (blocks=true):** 16
  - `feasibility-verdict` (min-conf 85) — highest threshold; CTO's central judgment
  - `tech-classification` (min-conf 80) — governs the document; fill first
  - `current-state` (min-conf 75) — brownfield/hybrid path; N/A if greenfield
  - `tech-foundation` (min-conf 75) — greenfield/hybrid path; N/A if brownfield
  - `architectural-impact` (min-conf 75)
  - `nfr-feasibility` (min-conf 75)
  - `hard-constraints` (min-conf 75)
  - `tech-risks` (min-conf 75)
  - `adrs` (min-conf 75)
  - `po-questions` (min-conf 70)
  - `affected-systems` (min-conf 70)
  - `integrations` (min-conf 70)
  - `alternatives` (min-conf 70)
  - `testability-observability` (min-conf 70)
  - `effort-cost` (min-conf 70)
  - (one of `current-state` / `tech-foundation` may clear via N/A depending on classification)
- **Non-blocking sections (blocks=false):** 4
  - `meta` (min-conf 0, kind=meta)
  - `revisions` (min-conf 0, kind=meta)
  - `build-vs-buy` (min-conf 0, kind=capture)
  - `discovery-path` (min-conf 0, kind=capture)
- **Default confidence threshold (X):** 70
- **Sections above default threshold:** `feasibility-verdict` (85), `tech-classification` (80), `current-state` (75), `tech-foundation` (75), `architectural-impact` (75), `nfr-feasibility` (75), `hard-constraints` (75), `tech-risks` (75), `adrs` (75)

<!-- END OF DOCUMENT -->
