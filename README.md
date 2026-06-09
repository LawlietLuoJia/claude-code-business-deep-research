# Business Deep Research — Claude Code Skill

[中文文档](README_zh.md)

A structured deep-research skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that produces evidence-backed business research reports with multi-source verification, explicit gap acknowledgment, and framework-driven analysis.

## The Problem

LLM search tools give you answers. Business decisions need evidence.

A quick lookup won't tell you whether a market is worth entering, how a competitor built their moat, or what regulatory risks lie ahead. Most research tools produce shallow summaries that look convincing but lack rigor — no cross-referencing, no gap acknowledgment, no structured methodology.

**Business Deep Research applies management consulting methodology to LLM-powered research**, producing structured artifacts that withstand scrutiny.

## What Makes This Different

### Five Research Lenses, Not One Workflow

The skill selects a framework based on the shape of your question — not a one-size-fits-all pipeline:

| Research Shape | Framework | What It Produces |
|---|---|---|
| How did we get here? What's the trajectory? | Evolution Lens | Historical arc, inflection points, path dependencies |
| Who else does this? What's defensible? | Competitive Lens | Peer map, moat analysis, positioning matrix |
| How big is the opportunity? What's the structure? | Market Lens | TAM/SAM, value chain, regulatory landscape |
| What should we do? What are the options? | Consulting Framework | Issue tree, hypothesis testing, recommendation chain |
| What are people saying? What patterns emerge? | Research Synthesis | Thematic analysis, sentiment clusters, gap map |

### Multi-Round Retrieval with Quality Gates

Not "search once and write." The skill runs multiple retrieval rounds, each with explicit quality checks:

- **Gate 1**: Is the source pool sufficient for the chosen framework?
- **Gate 2**: Does the evidence support the framework's prerequisites?
- **Gate 3**: Are gaps explicitly acknowledged before synthesis?

If a gate fails, the skill iterates — refining queries, expanding scope, or flagging limitations.

### Explicit Gap Acknowledgment

Every report includes a structured "Assumptions & Gaps" section. The skill doesn't pretend to know what it doesn't — it surfaces what's missing, what's uncertain, and what would need primary research to resolve.

### Free Toolchain, No Vendor Lock-in

Designed to work with freely available search tools. No paid API dependencies. The skill adapts its retrieval strategy to whatever search tools are available in your Claude Code environment.

### Structured Artifacts, Not Chat Prose

Outputs are structured documents, not conversational text:

| Artifact | Purpose |
|----------|---------|
| **Research Brief** | Scoping document — question, depth profile, constraints |
| **Search Log** | Every query, every source, why it was included or excluded |
| **Report** | Framework-driven analysis with inline citations |
| **Assumptions & Gaps** | What we don't know, what we assumed, what needs validation |

### Chinese-First Writing Quality

Built-in `writing-style-cn.md` reference ensures Chinese reports read naturally — not machine-translated. English reports follow the same structural rigor.

## Installation

```bash
# Project-level (recommended — keeps research domain-scoped)
cp -r . /your-project/.claude/skills/business-deep-research/

# Global
cp -r . ~/.claude/skills/business-deep-research/
```

## Usage

Trigger phrases:

```
深度研究 / 商业研究 / 竞品分析 / 市场研究 / 课题研究 / 研究报告
deep research / competitive research / market analysis / business decision memo
```

### Workflow

1. **Scope** → Define question, select framework, set depth profile
2. **Search** → Multi-round retrieval with quality gates at each stage
3. **Analyze** → Apply chosen lens to structured evidence
4. **Synthesize** → Write report with inline citations and gap analysis
5. **Review** → Quality check against evaluation rubric

## Project Structure

```
business-deep-research/
├── SKILL.md                          # Skill definition
├── agents/openai.yaml                # Agent configuration
├── assets/templates/                 # 4 structured output templates
│   ├── research-brief-template.md    #   Research scope document
│   ├── search-log-template.md        #   Source audit trail
│   ├── report-template.md            #   Framework-driven report
│   └── assumptions-and-gaps-template.md  # Gap analysis
├── evals/                            # Evaluation & quality rubrics
│   ├── evals.json
│   ├── evaluation-rubric.md
│   └── baseline-pressure-notes.md
├── references/                       # 14 reference documents
│   ├── framework-selector.md         #   Framework routing logic
│   ├── competitive-lens.md           #   Competitive analysis methodology
│   ├── market-lens.md                #   Market structure analysis
│   ├── evolution-lens.md             #   Historical trajectory analysis
│   ├── consulting-problem-solving.md #   Hypothesis-driven problem solving
│   ├── research-synthesis-lens.md    #   Qualitative data synthesis
│   ├── search-quality.md             #   Source quality assessment
│   ├── strict-verification.md        #   Evidence verification protocol
│   ├── retrieval-rounds.md           #   Multi-round search strategy
│   ├── writing-style-cn.md           #   Chinese writing style guide
│   └── ...                           #   + 4 more
└── schemas/                          # 4 JSON schemas for structured data
    ├── source.schema.json            #   Source metadata
    ├── evidence.schema.json          #   Evidence structure
    ├── claim.schema.json             #   Claim structure
    └── run-manifest.schema.json      #   Research run metadata
```

## License

MIT
