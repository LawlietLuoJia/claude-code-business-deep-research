# Output Contract

## Run Folder

Use the local project convention when it exists. In the BankCRM workbench, create a run folder under:

```text
outputs/research/YYYYMMDD-HHMM-<topic>/
```

Keep the folder name stable after Gate 1 so all artifacts point to the same run.

## Required Files

| File | Purpose |
|---|---|
| `research_brief.md` | Research question, decision context, scope, success criteria, subquestions, assumptions, first search plan |
| `search_log.md` | Search route, query intent, tool used, results status, skipped routes, fallback reason, remaining gaps |
| `sources.jsonl` | One canonical record per source |
| `evidence.jsonl` | Evidence spans, facts, data points, or observations linked to source IDs |
| `assumptions_and_gaps.md` | Assumptions, weak evidence, contradictions, unresolved questions, explicit limitations |
| `report.md` | Decision-ready commercial report |

For strict or restartable runs, also create the optional files described in [strict-verification.md](strict-verification.md):

| File | Purpose |
|---|---|
| `claims.jsonl` | Claim-level support ledger for material factual, synthesis, recommendation, and speculation rows |
| `run_manifest.json` | Stable run identity, scope state, selected lenses, artifact paths, tool-route notes, continuation state |

For long reports, also create the optional files described in [long-report.md](long-report.md):

| File | Purpose |
|---|---|
| `section_plan.md` | Frozen long-form section plan, section purpose, evidence needs, and continuation boundaries |
| `section_status.md` | Completed and pending sections, unresolved contradictions, next retrieval or synthesis tasks, final/partial status |
| `partial_report.md` | Used only when a long run stops before a decision-ready `report.md` exists |

Do not write a placeholder `report.md`. A long run that cannot finish a substantive decision-ready draft should leave `partial_report.md` plus continuation state instead.

## Research Brief Additions

During framing, add the selected depth profile from [depth-profile.md](depth-profile.md):

- Profile: Brief, Standard, or Deep
- Reason for the profile
- What the profile changes about retrieval, verification, gates, or deliverable shape
- What the profile does not answer

After initial evidence review and before Gate 2, add the framework selection record from [framework-selector.md](framework-selector.md):

- Primary lens
- Selected framework
- Why this framework fits the decision
- Evidence prerequisites
- Supporting lens or framework, if any
- Rejected frameworks
- Where it appears in the report

For strict or restartable runs, mirror the same selection in `run_manifest.json`.

## Search Log Additions

When using soft retrieval rounds from [retrieval-rounds.md](retrieval-rounds.md), record each round's objective and whether it was used, compressed, skipped, failed, or escalated. Skipped rounds need a reason.

## Source Record

Write one JSON object per line:

```json
{"source_id":"S001","url":"https://example.com","title":"Source title","publisher":"Publisher","published_at":"2026-05-01","accessed_at":"2026-05-22","source_type":"primary|secondary|lead","authority_reason":"why this source matters","bias_or_limit":"known bias, missing date, vendor claim, or none"}
```

Use stable source IDs. Do not let bibliography display numbers replace source IDs in the evidence pack.
Sequential readable IDs such as `S001` and `E001` are acceptable for normal runs. For strict, multi-session, or continuation-heavy work, prefer stable IDs that remain valid if rows are appended or report sections are revised.

## Evidence Record

Write one JSON object per line:

```json
{"evidence_id":"E001","source_id":"S001","subquestion":"What this evidence answers","evidence_type":"quote|fact|metric|observation","excerpt":"short exact excerpt or normalized fact","locator":"section, page, timestamp, or heading","supports":"finding or hypothesis label","confidence":"high|medium|low","note":"why it matters or what remains uncertain"}
```

Keep excerpts short and record normalized facts when quoting is unnecessary. If a claim depends on inference across evidence rows, say so in the report.

## Minimum Report Shape

Use the report template unless the user requests a different deliverable:

1. Executive answer
2. Research scope and method
3. Findings and evidence
4. Analysis through selected lens
5. Business implications or recommendations
6. Risks, alternatives, contradictions, and gaps
7. Source note or bibliography pointer

## Delivery Sweep

Do one report-level sweep before handoff. For each high-materiality claim that changes a recommendation, prioritization, risk view, market conclusion, or decision gate:

1. Point it to evidence IDs or a clearly identified source trail.
2. Mark it as inference when it depends on interpretation across evidence.
3. Move it into the gap register when public evidence does not support it strongly enough.

The default contract does not require a full claim ledger. Add one only when the task needs heavier verification or the comparison workflow already produces it.

## Schemas

The `schemas/` folder contains lightweight contracts for `sources.jsonl`, `evidence.jsonl`, optional `claims.jsonl`, and optional `run_manifest.json`. Use them as a shape guard. Do not let schema validation replace source judgment, contradiction handling, or claim review.
