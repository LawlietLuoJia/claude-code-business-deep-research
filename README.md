# Business Deep Research — Claude Code Skill

[中文文档](README_zh.md)

A structured deep-research skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that guides LLM-powered research through a consulting-style methodology, producing structured reports with cited sources and acknowledged gaps.

## Background

When you need to research a business question — entering a new market, evaluating a competitor, assessing a technology trend — a single LLM search gives you a surface-level answer. The information might be useful, but it's not sufficient for decision-making.

The gaps are structural:

- **No methodology**: The LLM searches and summarizes, but doesn't follow a systematic process
- **No cross-referencing**: Claims from one source aren't verified against others
- **No gap tracking**: The output doesn't tell you what it couldn't find
- **No structured output**: You get a wall of text, not documents you can share with stakeholders

Business Deep Research addresses these by embedding a research methodology into the skill itself.

## How It Works

The skill guides the LLM through a structured process modeled on management consulting research:

### Step 1: Scope the Research

Before searching, the skill helps define:
- The precise research question
- The depth level needed (quick scan vs. full deep-dive)
- Which research framework fits the question shape
- What deliverables to produce

### Step 2: Multi-Round Retrieval

Instead of one search, the skill runs multiple retrieval rounds. Each round has a quality gate:

- After round 1: Is the source pool sufficient to proceed?
- After round 2: Does the evidence support the chosen framework's requirements?
- After round 3: Are gaps identified before moving to synthesis?

If a gate fails, the skill adjusts queries or flags limitations honestly.

### Step 3: Framework-Driven Analysis

The skill selects one of five research frameworks based on the question:

| Question Shape | Framework | When to Use |
|---|---|---|
| How did X evolve to its current state? | Evolution Lens | Understanding history, trajectory, path dependencies |
| How does X compare to peers? | Competitive Lens | Peer analysis, moat evaluation, positioning |
| What's the structure of X's market? | Market Lens | Market sizing, value chain, regulation, risk |
| What should we do about X? | Consulting Framework | Decision memo, options analysis, recommendation |
| What patterns exist in qualitative data? | Research Synthesis | Interview/survey/feedback analysis |

The framework determines what evidence to prioritize and how to structure the analysis. A second framework can be added if it addresses a distinct sub-question.

### Step 4: Structured Output

The skill produces four documents, not a single chat response:

| Document | Content |
|----------|---------|
| **Research Brief** | Question, scope, depth level, chosen framework, constraints |
| **Search Log** | Every query run, every source found, inclusion/exclusion rationale |
| **Report** | Framework-driven analysis with inline citations to sources |
| **Assumptions & Gaps** | What assumptions were made, what couldn't be verified, what needs primary research |

The "Assumptions & Gaps" section is particularly important: it tells you what the research *doesn't* know, so you can make informed decisions about what to trust and what to verify independently.

### Step 5: Review

A quality check against the evaluation rubric before finalizing.

## Design Decisions

**Why framework-driven?** Without a framework, research tends to be unfocused — gathering information without a clear analytical structure. The framework keeps the research targeted and the output organized.

**Why multiple retrieval rounds?** One search rarely surfaces sufficient evidence. Multiple rounds allow the skill to refine queries based on what it found (or didn't find) previously.

**Why explicit gap acknowledgment?** LLMs tend to present findings with false confidence. Forcing the skill to document what it *doesn't* know counteracts this tendency and gives the reader honest context.

**Why structured artifacts?** Research output often needs to be shared with stakeholders who weren't in the conversation. Structured documents are more useful than chat logs.

**Free toolchain?** The skill uses whatever search tools are available in the Claude Code environment — no paid API dependencies. It adapts its retrieval strategy accordingly.

## Installation

```bash
# Project-level (recommended)
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

## Project Structure

```
business-deep-research/
├── SKILL.md                          # Skill definition
├── agents/openai.yaml                # Agent configuration
├── assets/templates/                 # 4 output templates
│   ├── research-brief-template.md
│   ├── search-log-template.md
│   ├── report-template.md
│   └── assumptions-and-gaps-template.md
├── evals/                            # Evaluation criteria
│   ├── evals.json
│   ├── evaluation-rubric.md
│   └── baseline-pressure-notes.md
├── references/                       # 14 reference documents
│   ├── framework-selector.md         # Framework routing logic
│   ├── competitive-lens.md
│   ├── market-lens.md
│   ├── evolution-lens.md
│   ├── consulting-problem-solving.md
│   ├── research-synthesis-lens.md
│   ├── search-quality.md
│   ├── strict-verification.md
│   ├── retrieval-rounds.md
│   ├── writing-style-cn.md           # Chinese writing quality
│   ├── depth-profile.md
│   ├── output-contract.md
│   ├── runtime-adapters.md
│   └── long-report.md
└── schemas/                          # 4 JSON schemas
    ├── source.schema.json
    ├── evidence.schema.json
    ├── claim.schema.json
    └── run-manifest.schema.json
```

## License

MIT
