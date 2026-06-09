---
name: business-deep-research
description: Use when a user needs commercial deep research for a company, product, competitor set, market, business problem, technical topic, policy topic, due-diligence question, or decision memo that needs multi-source evidence, explicit gaps, and business implications. Trigger on "深度研究", "商业研究", "竞品分析", "市场研究", "课题研究", "研究报告", "deep research", "competitive research", "market analysis", or "business decision memo" when a quick lookup is insufficient.
---

# Business Deep Research

Run commercial deep research that a decision maker can audit. The core rule is evidence before polish: frame the decision, capture sources and evidence, then choose the analysis lens and write the report.

## When To Use

Use for multi-source business research where the user needs judgment, not a quick lookup:

- Company, product, concept, or technology trajectory and present position
- Competitor landscape, peer benchmarking, and strategic comparison
- Market opportunity, industry dynamics, and scenario or risk research
- Technical or policy topics translated into commercial implications
- User-research or feedback corpora that must become decision-ready findings

Do not use for one-off fact lookup, debugging, pure academic paper production, or writing from source material the user already summarized enough to answer directly.

## Default Workflow

1. **Frame.** Convert the request into a research question, decision context, scope, success criteria, known constraints, key subquestions, assumptions, and a Brief/Standard/Deep profile. Draft `research_brief.md`.
2. **🔴 CHECKPOINT · Gate 1.** Show the research brief and ask the user to confirm scope before broad retrieval. For a full research run, state that the run will keep `sources.jsonl`, `evidence.jsonl`, and `search_log.md` so the user knows conclusions will be auditable. If the user explicitly requests an autonomous run, state the assumed scope and continue; record the gate as `waived_by_user` or `assumed_for_autonomous_run` in `search_log.md`.
3. **Plan search.** Build a search matrix per subquestion: likely primary sources, secondary or lead sources, languages, geographies, recency needs, opposing evidence, and data gaps to watch.
4. **Retrieve in rounds.** Run breadth → depth → verification rounds for Standard and Deep profiles. Skip to verification-only for Brief profiles or when the subquestion set has ≤2 items. Record the round decision and reason in `search_log.md`.
5. **Persist evidence.** Register sources and evidence before writing report conclusions. High-materiality findings need traceable evidence IDs or explicit gap labels.
6. **Select lenses.** Use one primary framework and only the supporting lenses justified by evidence and task shape. Record why the framework was selected and which common frameworks were rejected. Do not run every framework by habit.
7. **🔴 CHECKPOINT · Gate 2.** Present preliminary findings, evidence gaps, selected lens, and report outline. Confirm direction before final report drafting unless the user already authorized an autonomous run; if waived, record why in `search_log.md`. Brief profile may compress Gate 2, but it cannot skip evidence capture, inference/gap labeling, or material uncertainty disclosure.
8. **Write and critique.** Draft the report, challenge weak claims and alternative interpretations, separate facts from inferences, revise, and package the artifacts.

## Failure Modes

| 触发条件 | 一线修复 | 仍失败兜底 |
|----------|---------|-----------|
| 搜索返回空或无关结果 | 换同义词/英文关键词重试，切换搜索引擎 | 在 `assumptions_and_gaps.md` 记录 Gap，用推理替代但标注 Inference |
| 多个来源数据矛盾 | 优先采信一手来源（官方财报/监管文件） | 在报告中标明矛盾，分别引用，不做强制取舍 |
| 关键指标找不到公开数据 | 用行业估算范围替代点值，标注数据源层级 | 降级为区间估计或 Gap，不编造精确数字 |
| Tavily/OpenCLI 不可用 | 按 `runtime-adapters.md` 降级链切换工具 | 用 TinyFish Search/Fetch 兜底，记录降级路径 |
| 报告超 10000 词未完成 | 切换 long-report 模式，生成 `partial_report.md` | 在 `section_status.md` 标记未完成章节和后续检索路线 |
| 深度档案不匹配决策风险 | 向上或向下调整档案，记录调整原因 | 在 Gate 2 向用户说明档案调整，获取确认 |

## Artifact Scope

Use the workspace output convention if one exists. In this workspace, default to `outputs/research/YYYYMMDD-HHMM-<topic>/`.

For Brief runs, create only the artifacts needed to keep the answer auditable: at minimum `research_brief.md` or an in-message brief, `search_log.md` when retrieval is performed, and visible source/evidence references or explicit gaps. Do not force a complete evidence package for a narrow orientation task.

For Standard, Deep, autonomous, restartable, high-stakes, or user-requested full runs, create these files:

- `research_brief.md`
- `search_log.md`
- `sources.jsonl`
- `evidence.jsonl`
- `assumptions_and_gaps.md`
- `report.md`

Load [output-contract.md](references/output-contract.md) before creating artifacts. Reuse the templates in `assets/templates/` for `research_brief.md`, `search_log.md`, `report.md`, and `assumptions_and_gaps.md`.

For high-stakes work, due diligence, long reports, disputed facts, restartable research, or a user request for claim-level checking, load [strict-verification.md](references/strict-verification.md) and apply its material-claim triage before drafting. For a report expected to exceed 10,000 words or to be delivered in sections, load [long-report.md](references/long-report.md).
When long-report mode is active, persist `section_plan.md` and `section_status.md`; write `partial_report.md` instead of a placeholder `report.md` if the run stops before a substantive decision-ready draft exists.

## Search Quality

Load [depth-profile.md](references/depth-profile.md) during framing. Load [search-quality.md](references/search-quality.md) for source hierarchy, search matrix design, verification rules, source-chain independence, and contradiction handling. Load [retrieval-rounds.md](references/retrieval-rounds.md) when planning or logging retrieval. Load [runtime-adapters.md](references/runtime-adapters.md) before using search tools so tool names match the current runtime; do not write tool calls that exist only in another runtime.

Default policy:

- Prefer Tavily search/extract for evidence discovery and page extraction when available.
- Treat Tavily research, AI answers, news summaries, and social posts as reconnaissance or leads unless the underlying evidence is captured.
- Use OpenCLI plus Smart Search for platform-specific, Chinese, social, news, or vertical sources when the research question needs them.
- Use TinyFish only for free `Search` and `Fetch` in the default path.
- Do not use TinyFish Agent or Browser unless the user explicitly approves a credit-consuming escalation.

## Framework Selector

After evidence review, load [framework-selector.md](references/framework-selector.md) and only the lens references needed:

| Research shape | Primary reference |
|---|---|
| Origin, evolution, historical decisions, present position | [evolution-lens.md](references/evolution-lens.md) |
| Peer set, comparison, moat, positioning | [competitive-lens.md](references/competitive-lens.md) |
| Market definition, opportunity, industry structure, regulation, risk | [market-lens.md](references/market-lens.md) |
| Business problem, options, recommendation chain | [consulting-problem-solving.md](references/consulting-problem-solving.md) |
| Interviews, surveys, tickets, feedback, qualitative themes | [research-synthesis-lens.md](references/research-synthesis-lens.md) |

Choose one primary lens. Add a supporting lens only when it answers a distinct subquestion and does not duplicate the primary lens.
Before Gate 2, record the primary lens, selected framework, evidence prerequisites, rejected frameworks, and where the framework will appear in the report.

## Report Standard

Write in the user's language. Chinese is the default when the user writes in Chinese.
For Chinese reports, load [writing-style-cn.md](references/writing-style-cn.md).

The report should open with the answer that matters, then show evidence, reasoning, implications, limits, and next steps. Mark:

- `Fact`: directly supported by evidence
- `Inference`: interpretation drawn from cited evidence
- `Gap`: relevant question not supported well enough

Commercial rigor means the recommendation chain is auditable. It does not require an academic citation style, a mandatory claim ledger, or a large report when the decision can be supported by a shorter report.

## Do Not

1. **不把厂商宣传当事实**: 厂商官网、PR 稿、融资 BP 中的数据点必须与独立来源交叉验证。未经交叉验证的数字只能标注为「厂商声明」，不能作为 Fact 引用
2. **不先选框架再找证据**: 框架选择必须在证据收集之后（Step 6），不跳到 Step 6 先选框架
3. **不跳过 Gate 直接写报告**: Gate 1 和 Gate 2 是硬性检查点，即使用户要求自主运行也必须记录 `waived_by_user` 并说明范围假设
4. **不用 AI 摘要替代一手证据**: Tavily Research、AI Answers、新闻摘要只能作为线索（lead），不能替代一手来源的独立证据捕获
5. **不粉饰 Gap**: 证据不足时直接标注 Gap，不用模糊措辞掩盖。检索失败时记录失败路径和下一步建议
6. **不堆砌框架**: 只选一个主框架，辅助框架仅在回答独立子问题时添加。禁止「五个框架全跑一遍」的惯性
7. **不为凑深度档案而虚增来源**: Brief 档案不需要强行凑 20 条来源。来源数量服务于决策风险，不服务于形式
8. **不在无证据时给出确定性建议**: 如果核心假设缺乏证据支撑，推荐级别必须降级为「有条件建议」或「需进一步验证」
9. **不混合 Fact 和 Inference 标注**: 每个 claim 只能有一个标注。如果同时有事实支撑和推理成分，拆分为两条独立 claim
10. **不跳过矛盾和反证据**: 搜索计划必须包含对立证据检索（Step 3 "opposing evidence"）。报告必须呈现反方视角

## Quality Check

Before delivery:

1. Confirm both gates were honored or explicitly waived by the user.
2. Check core facts rely on primary or high-authority sources where available.
3. Check the search log records tool route, query intent, failures, skipped routes, and fallback reason.
4. Sweep the report's high-materiality claims before delivery: each one must point to evidence, be marked as inference, or be restated as a gap. Do this even when no claim ledger is created.
5. Check material conclusions point back to evidence or are marked as inference/gap.
6. Check contradictions, weak public data, time-sensitive claims, and geographic limits are visible.
7. Ask two compressed devil's-advocate questions: what disconfirming evidence may have been skipped, and which recommendation would weaken most if public evidence is overstated?
8. Check the selected frameworks explain the answer instead of cluttering it.
9. Check the framework selection record exists and names rejected frameworks or explains why no named framework was needed.
10. Check the selected depth profile matched the user's decision risk and did not create fixed source-count padding.
11. Check retrieval rounds were used, compressed, or skipped for a stated reason.
12. If retrieval degraded on a decision-critical question, state the gap and the next evidence route instead of polishing uncertainty away.
