# Strict Verification

Load this reference when research is high-stakes, due-diligence-like, long-running, restartable, disputed, or the user asks for claim-level verification.

Strict mode strengthens auditability. It does not change the default research method or force academic formatting.

## Extra Artifacts

Create the default evidence package plus:

| File | Purpose |
|---|---|
| `claims.jsonl` | Material claims linked to sources and evidence |
| `run_manifest.json` | Run state, artifact paths, selected lens, scope assumptions, continuation notes |

Use `schemas/claim.schema.json` and `schemas/run-manifest.schema.json` as the record shape.

## Claim Ledger

Register only claims that matter to a decision:

- Factual claims that carry a metric, date, legal obligation, capability, purchase signal, or source-sensitive comparison
- Synthesis claims that change positioning, opportunity size, risk view, or scenario
- Recommendations and signposts that depend on specific evidence rows
- Speculation that must stay visibly weaker than fact

Do not ledger every sentence.

## Material-Claim Triage

Before drafting, scan the evidence and planned report for claims that deserve verification. Prioritize:

- Metrics, rankings, market sizes, growth rates, funding, revenue, users, customers, adoption, benchmark results, or performance numbers
- Dates, sequence claims, regulatory obligations, legal thresholds, policy status, standards, or enforcement actions
- Product or technical capability claims that affect buy/build/partner decisions
- Comparative claims such as "leader", "only", "largest", "faster", "cheaper", "more secure", or "better suited"
- Causal claims, risk claims, and recommendations that depend on a specific evidence pattern
- Claims sourced from vendor marketing, social posts, snippets, AI summaries, anonymous commentary, or a single secondary report

For each triaged claim, decide whether to register it in `claims.jsonl`, downgrade it in the report, or move it to `assumptions_and_gaps.md`.

Each row should identify:

- Stable `claim_id`
- `claim_type`: `factual`, `synthesis`, `recommendation`, or `speculation`
- The claim text
- Source IDs and evidence IDs that support it
- Support status: `supported`, `partial`, `gap`, `contradicted`, or `needs_review`
- The reason when support is weak

Optional fields may be added when useful:

- `verification_focus`: `metric`, `date`, `obligation`, `capability`, `comparison`, `causal`, `recommendation`, or `source_sensitive`
- `primary_trace_status`: `found`, `partial`, `missing`, `circular`, or `not_applicable`
- `source_independence`: `independent`, `shared_origin`, `single_chain`, `vendor_only`, or `unknown`
- `counter_evidence_ids`: evidence IDs that weaken or contradict the claim
- `statistical_context`: unit, denominator, geography, time period, sample, dataset, or methodology caveat
- `verification_note`: concise explanation of the final confidence judgment

These fields are optional guardrails, not a reason to ledger every sentence.

## Verification Pass

For each material claim:

1. Identify the responsible primary source or mark why it is unavailable.
2. Check whether supporting sources are independent or share the same origin.
3. Search for counter-evidence or an alternative interpretation when the claim changes the decision.
4. For statistical claims, check unit, denominator, time period, geography, sample or dataset, and methodology.
5. Keep contradictions and partial support visible in `claims.jsonl` and `assumptions_and_gaps.md`.
6. Downgrade unsupported or weakly supported wording before the final report.

## Strict Review

Before delivery:

1. Check every material factual claim has evidence or is downgraded to a gap.
2. Check synthesis claims name the evidence pattern and alternative interpretation.
3. Check recommendations do not outrun their weakest dependency.
4. Check contradicted or partial claims remain visible in `assumptions_and_gaps.md`.
5. Check claims that depend on news, social, vendor marketing, or AI reconnaissance have stronger support before they carry the conclusion.

If a deterministic checker exists in the runtime, it may validate ledger shape, missing links, and obvious unsupported factual rows. Treat it as a guardrail, not as proof that the research judgment is correct.

## Run Manifest

Use the manifest when a run may continue across sessions or outputs:

- Topic and decision context
- Gate status and user waivers
- Date range and language/geography scope
- Selected primary lens and any supporting lens
- Artifact paths
- Search routes used, skipped, failed, and escalated
- Strict-mode status and open gaps
- Continuation pointer for the next section or delta-search row
