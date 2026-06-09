# Long Report Profile

Load this profile when the user requests an exhaustive report, a multi-section formal report, a deep memo likely to exceed roughly 10,000 words, or a run that may need continuation.

Long reports need stronger structure, not more framework filler.

## Use With

- The normal two gates unless the user explicitly waives them
- The same evidence package
- `strict-verification.md` when sections carry high-materiality claims or the run may resume later

## Long-Form Workflow

1. Freeze the report outline at Gate 2 with section purpose, decision use, likely evidence rows, and expected limits.
2. Create `section_plan.md` before drafting: section list, section purpose, required evidence IDs or gaps, planned claim checks, and continuation boundaries.
3. Draft section by section from the evidence package. Run delta search when a section exposes a real gap.
4. Update `section_status.md` after each substantive section: completed sections, pending sections, unresolved contradictions, next retrieval task, and whether the current report is final or partial.
5. After each major section, sweep facts, inferences, gaps, counterevidence, and repeated claims before continuing.
6. Run a final cross-section synthesis pass so the report has one recommendation chain instead of disconnected chapters.

## Persistence Rules

Long reports are more likely to hit runtime limits. Persist progress in restartable artifacts rather than pretending the report is finished.

- Do not create a placeholder `report.md`.
- Write `report.md` only when it contains the executive answer and substantive completed sections.
- If the run stops before a decision-ready draft exists, write `partial_report.md` instead and mark the continuation state in `section_status.md` or `run_manifest.json`.
- For long plus strict runs, append section-level claim rows as sections finish. Do not wait for one final claim-ledger pass.
- If evidence extraction is incomplete, leave the affected section as pending and record the next search route. Do not fill the gap with generic analysis.

## Long-Form Shape

Use the compact default report when it is enough. For long form, expand only the sections the decision needs:

1. Executive answer and decision implications
2. Research brief, scope, method, and evidence quality note
3. Context or market/problem map
4. Findings by subquestion
5. Analysis through the selected primary lens
6. Alternatives, contradictions, scenarios, and risks
7. Recommendation chain, signposts, and next evidence route
8. Evidence-pack pointer and appendices as needed

Add charts, HTML, PDF, slides, or appendices only when the user needs that deliverable. Packaging polish must not hide weak public evidence.

## Continuation State

Use this compact shape in `section_status.md` or `run_manifest.json`:

```json
{"status":"partial|final","completed_sections":["section id"],"pending_sections":["section id"],"open_gaps":["gap id"],"next_actions":["search or synthesis step"],"safe_resume_from":"section id or task"}
```

When resuming, load `section_plan.md`, `section_status.md`, `sources.jsonl`, `evidence.jsonl`, and optional `claims.jsonl` before writing more prose.

## Long-Form Guardrails

- Do not inflate length to hit a word target.
- Do not load every analytical framework to fill chapters.
- Do not repeat source summaries section after section; synthesize by claim and decision impact.
- Do not auto-continue through an unstable outline. Reconfirm direction if the answer shape changes materially.
- Do not mark a long report complete if only an outline, evidence pointer, or placeholder has been written.
