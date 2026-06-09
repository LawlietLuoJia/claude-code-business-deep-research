# Runtime Adapters

## Runtime Check

Use the tools visible in the current runtime. Do not write tool calls that exist only in the other runtime.

## Codex Adapter

Default discovery order:

1. Use Tavily for evidence discovery and extraction when it is configured in the current Codex environment.
2. When the local Tavily CLI is available, start with `tvly search "<query>" --json` for discovery and `tvly extract "<url>" --json` for source text. Inspect command help before relying on non-basic flags or provider behavior.
3. For OpenCLI searches, load or follow `opencli-usage` and `smart-search`; inspect `opencli list` and command help before live adapter calls.
4. Use TinyFish only as `tinyfish search` and `tinyfish fetch` in the default path.
5. Use direct official or primary pages once discovered and record evidence from the page, not from the search snippet.

If network or provider access fails, keep a search-log entry and continue with the best available primary sources or user-provided materials. If a decision-critical row remains unsupported, package it as a gap or ask for a source instead of hiding a degraded retrieval path.

## Claude Adapter

Default discovery order:

1. Use Tavily search and extract skills for evidence retrieval when available.
2. Use Tavily research only for reconnaissance, query expansion, and coverage checks.
3. Use `/opencli-usage` plus `/smart-search` for platform-specific and Chinese vertical routes.
4. Use `/use-tinyfish` only for TinyFish Search and Fetch by default.
5. Treat TinyFish Agent and Browser as explicit approval paths because they can consume credits.

## Paid Escalation Boundary

Before a credit-consuming or paid escalation:

1. State why normal search or fetch is insufficient.
2. Name the tool and cost boundary.
3. Ask for explicit approval.
4. Record the decision in `search_log.md`.
