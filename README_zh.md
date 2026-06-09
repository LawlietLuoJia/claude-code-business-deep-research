# Business Deep Research — Claude Code 商业深度研究 Skill

[English](README.md)

面向 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 的结构化深度研究技能，将咨询式研究方法论嵌入 LLM 研究流程，产出带引用来源和缺口标注的结构化报告。

## 背景

当你需要研究一个商业问题——进入新市场、评估竞争对手、研判技术趋势——一次 LLM 搜索给你的是浅层答案。信息可能有用，但不足以支撑决策。

这些差距是结构性的：

- **没有方法论**：LLM 搜索然后总结，但不遵循系统化的流程
- **没有交叉验证**：来自一个来源的论断不会与其他来源比对
- **没有缺口追踪**：输出不会告诉你它找不到什么
- **没有结构化输出**：你得到一大段文字，而不是可以分享给利益相关方的文档

Business Deep Research 通过将研究方法论嵌入技能本身来解决这些问题。

## 工作原理

技能引导 LLM 遵循基于管理咨询研究方法论的结构化流程：

### 第一步：确定研究范围

搜索之前，技能帮助明确：
- 精确的研究问题
- 所需深度（快速扫描 vs. 全面深潜）
- 哪个研究框架匹配问题的形态
- 要产出哪些交付物

### 第二步：多轮检索

不是一次搜索，而是多轮检索。每轮之后有质量门禁：

- 第 1 轮后：来源池是否足够继续？
- 第 2 轮后：证据是否支撑所选框架的前提条件？
- 第 3 轮后：进入综合阶段前是否已识别缺口？

门禁不通过则调整查询，或如实标记局限性。

### 第三步：框架驱动分析

技能根据问题形态选择五个研究框架之一：

| 问题形态 | 框架 | 适用场景 |
|---------|------|---------|
| X 是如何演化到当前状态的？ | 演化视角 | 理解历史、轨迹、路径依赖 |
| X 与同业相比如何？ | 竞争视角 | 同业分析、护城河评估、定位 |
| X 所在市场的结构是什么？ | 市场视角 | 市场规模、价值链、监管、风险 |
| 关于 X 我们该怎么做？ | 咨询框架 | 决策备忘、选项分析、建议 |
| 定性数据中有什么规律？ | 研究综合视角 | 访谈/问卷/反馈分析 |

框架决定优先收集什么证据、如何组织分析。如果有独立的子问题，可以叠加第二个框架。

### 第四步：结构化输出

技能产出四份文档，不是一段聊天文本：

| 文档 | 内容 |
|------|------|
| **研究简报** | 问题、范围、深度级别、所选框架、约束条件 |
| **搜索日志** | 每个查询、每个来源、包含/排除的理由 |
| **研究报告** | 框架驱动的分析，含行内来源引用 |
| **假设与缺口** | 做了哪些假设、哪些无法验证、哪些需要一手调研 |

"假设与缺口"部分尤为重要：它告诉你研究*不知道*什么，让你对哪些可以信任、哪些需要独立验证做出知情判断。

### 第五步：评审

最终输出前按评分标准做质量检查。

## 设计决策

**为什么框架驱动？** 没有框架的研究容易失焦——收集信息但没有清晰的分析结构。框架让研究有针对性、输出有组织。

**为什么多轮检索？** 一次搜索很少能获取足够的证据。多轮允许技能根据已找到（或未找到）的内容精炼查询。

**为什么要显式标注缺口？** LLM 倾向于用虚假的自信呈现结果。强制标注*不知道*的内容可以抵消这种倾向，给读者诚实的上下文。

**为什么结构化制品？** 研究产出通常需要分享给没有参与对话的利益相关方。结构化文档比聊天记录更有用。

**免费工具链？** 技能使用 Claude Code 环境中可用的任何搜索工具——无付费 API 依赖。它据此调整检索策略。

## 安装

```bash
# 项目级安装（推荐）
cp -r . /your-project/.claude/skills/business-deep-research/

# 全局安装
cp -r . ~/.claude/skills/business-deep-research/
```

## 使用方式

触发短语：

```
深度研究 / 商业研究 / 竞品分析 / 市场研究 / 课题研究 / 研究报告
deep research / competitive research / market analysis / business decision memo
```

## 项目结构

```
business-deep-research/
├── SKILL.md                          # Skill 定义
├── agents/openai.yaml                # Agent 配置
├── assets/templates/                 # 4 个输出模板
│   ├── research-brief-template.md
│   ├── search-log-template.md
│   ├── report-template.md
│   └── assumptions-and-gaps-template.md
├── evals/                            # 评估标准
│   ├── evals.json
│   ├── evaluation-rubric.md
│   └── baseline-pressure-notes.md
├── references/                       # 14 个参考文档
│   ├── framework-selector.md         # 框架路由逻辑
│   ├── competitive-lens.md
│   ├── market-lens.md
│   ├── evolution-lens.md
│   ├── consulting-problem-solving.md
│   ├── research-synthesis-lens.md
│   ├── search-quality.md
│   ├── strict-verification.md
│   ├── retrieval-rounds.md
│   ├── writing-style-cn.md           # 中文写作质量
│   ├── depth-profile.md
│   ├── output-contract.md
│   ├── runtime-adapters.md
│   └── long-report.md
└── schemas/                          # 4 个 JSON Schema
    ├── source.schema.json
    ├── evidence.schema.json
    ├── claim.schema.json
    └── run-manifest.schema.json
```

## 许可证

MIT
