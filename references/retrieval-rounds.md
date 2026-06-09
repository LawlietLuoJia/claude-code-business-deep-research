# Retrieval Rounds

Use soft retrieval rounds when planning or logging search. Rounds are conditional, gap-driven, and may be compressed or skipped.

## Rounds

1. **Breadth: source-family discovery.** Find the source families, terms of art, competing explanations, and obvious primary sources.
2. **Depth: strongest-source extraction.** Extract from the best sources and fill material gaps that affect the decision.
3. **Verification: material-claim cross-check.** Cross-check claims, metrics, obligations, comparisons, or recommendations that would change the answer.

## Rules

- Do not run rounds ritualistically. Skip or compress a round when the task is narrow, sources are already primary, or the selected profile is Brief.
- Record skipped or compressed rounds in `search_log.md` with the reason.
- Verification is for material claims, not for inflating source count.
- If public evidence is weak, use delta searches for the gap and keep unsupported conclusions as `Gap` or `Inference`.
- Treat vendor pages, social posts, AI summaries, and snippets as leads unless stronger evidence supports the claim.

## Search Log Fields

For each round, record:

- round name and objective
- query intents or source families
- tool route used, skipped, failed, or escalated
- accepted sources or evidence targets
- material gaps and next delta search, if any
