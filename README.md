# Business Deep Research — Claude Code Skill

[中文文档](README_zh.md)

A structured deep-research skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that produces evidence-backed business research reports with multi-source verification, explicit gaps, and framework-driven analysis.

Built for commercial due diligence, competitive analysis, market research, and decision memos that go beyond a quick lookup.

## Features

- **Framework-Driven Analysis**: Selects from 5 research lenses (Evolution, Competitive, Market, Consulting Problem-Solving, Research Synthesis)
- **Multi-Source Verification**: Cross-references evidence with strict citation requirements
- **Search Quality Gates**: Built-in quality checks at each research phase
- **Bilingual Output**: Supports both English and Chinese report writing
- **Artifact-Scoped**: Produces structured outputs — research brief, search log, report, assumptions & gaps
- **Free Toolchain**: Designed to work with freely available search tools (no paid API dependencies)

## Installation

Copy this directory into your Claude Code skills folder:

```bash
# Project-level (recommended)
cp -r . /your-project/.claude/skills/business-deep-research/

# Global
cp -r . ~/.claude/skills/business-deep-research/
```

## Usage

Trigger the skill with phrases like:

```
深度研究    # Chinese
商业研究
竞品分析
市场研究
```

```
deep research    # English
competitive research
market analysis
business decision memo
```

### Workflow

1. **Scope** → Define research question, depth profile, and deliverables
2. **Search** → Multi-round retrieval with quality gates
3. **Analyze** → Apply framework lens to structured evidence
4. **Synthesize** → Write report with citations, gaps, and implications
5. **Review** → Quality check against rubric

### Research Lenses

| Shape | Primary Lens | Reference |
|-------|-------------|-----------|
| Origin, evolution, history | Evolution Lens | `references/evolution-lens.md` |
| Peer comparison, moat | Competitive Lens | `references/competitive-lens.md` |
| Market definition, regulation | Market Lens | `references/market-lens.md` |
| Business problem, options | Consulting Framework | `references/consulting-problem-solving.md` |
| Qualitative data synthesis | Research Synthesis | `references/research-synthesis-lens.md` |

## Project Structure

```
business-deep-research/
├── SKILL.md                     # Skill definition
├── agents/
│   └── openai.yaml              # OpenAI-compatible agent config
├── assets/
│   └── templates/               # Output templates
│       ├── assumptions-and-gaps-template.md
│       ├── report-template.md
│       ├── research-brief-template.md
│       └── search-log-template.md
├── evals/                       # Evaluation & quality rubrics
│   ├── baseline-pressure-notes.md
│   ├── evals.json
│   └── evaluation-rubric.md
├── references/                  # Skill reference docs (14 files)
│   ├── competitive-lens.md
│   ├── consulting-problem-solving.md
│   ├── depth-profile.md
│   ├── evolution-lens.md
│   ├── framework-selector.md
│   ├── long-report.md
│   ├── market-lens.md
│   ├── output-contract.md
│   ├── research-synthesis-lens.md
│   ├── retrieval-rounds.md
│   ├── runtime-adapters.md
│   ├── search-quality.md
│   ├── strict-verification.md
│   └── writing-style-cn.md
└── schemas/                     # JSON schemas for structured data
    ├── claim.schema.json
    ├── evidence.schema.json
    ├── run-manifest.schema.json
    └── source.schema.json
```

## License

MIT
