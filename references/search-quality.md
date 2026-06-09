# Search Quality

## Principle

Retrieval is a research design problem. Use tools to reach the right evidence, not to inflate result count.

## Search Matrix

Before broad retrieval, create rows for:

| Field | What to decide |
|---|---|
| Subquestion | The decision-relevant question being answered |
| Primary sources | Official docs, filings, regulators, datasets, product docs, direct statements |
| Secondary sources | Reputable analysis, reporting, expert commentary, benchmark material |
| Lead sources | Social, community, AI synthesis, aggregators, snippets |
| Language and geography | Chinese, English, local regulation, global comparison |
| Recency | Current state, historical baseline, date-sensitive facts |
| Opposing evidence | Critics, failure cases, conflicting metrics, alternative explanation |
| Gap test | What remains unknown if the first pass fails |

## Source Hierarchy

Use this order for core claims when available:

1. Primary source with direct responsibility for the fact
2. Regulator, standards body, official dataset, audited filing, original research, or original product documentation
3. Reputable reporting or domain analysis that names its evidence
4. Practitioner or community material for use patterns, sentiment, operational detail, and leads
5. AI summaries, snippets, aggregators, and reposts as discovery only

Vendor claims may be primary for what the vendor says or ships, but not automatically neutral for market size, superiority, or customer outcome claims.

## Source Independence

For material conclusions, check whether supporting sources are actually independent evidence chains:

- Treat duplicated wire stories, reposted press releases, syndicated articles, copied charts, and reports citing the same dataset as one evidence chain.
- Separate `primary source`, `independent secondary analysis`, and `lead only` in the search log when the distinction affects confidence.
- Prefer at least one primary trace for metrics, legal obligations, product capabilities, funding, customer adoption, or source-sensitive comparisons.
- If a claim is supported only by vendor marketing, social posts, AI reconnaissance, snippets, or aggregators, keep it as `Inference`, `partial`, or `Gap` unless stronger evidence is captured.
- Record circular sourcing when sources cite each other without reaching the responsible original source.

## Retrieval Loop

1. Discover likely sources across independent subquestions.
2. Screen for authority, date, bias, independence, and answer fit.
3. Extract evidence from the best sources.
4. Update source and evidence artifacts immediately.
5. Mark contradictions and unanswered rows.
6. Run delta searches only for important gaps or alternative interpretations.

Use [retrieval-rounds.md](retrieval-rounds.md) when the run benefits from an explicit breadth/depth/verification search log. The rounds are soft: compress or skip them when the profile, evidence, or user need makes a full round unnecessary.

## Verification

- Verify time-sensitive facts against current source dates.
- Prefer independent support for material factual conclusions.
- A repeated syndicated article is one evidence chain, not many confirmations.
- Trace high-materiality claims back to the responsible primary source when available; record `found`, `partial`, `missing`, or `circular` when strict verification is active.
- Search for plausible counter-evidence before allowing a contested metric, capability claim, legal obligation, or recommendation dependency to carry the conclusion.
- For statistical claims, check the unit, denominator, time period, geography, sample or dataset, methodology, and whether the number was quoted out of context.
- When sources conflict, record the conflict, why each source may differ, and which decision consequence changes.
- If public evidence is weak, preserve the gap instead of converting it into a confident recommendation.

## Search Log

For each meaningful query or fetch route record:

- Timestamp or research batch
- Tool and source route
- Query intent, not only raw query text
- Outcome: success, partial, failed, skipped
- Why the result was accepted, discarded, or deferred
- Follow-up gap or fallback reason
