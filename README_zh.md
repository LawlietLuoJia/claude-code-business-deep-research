# Business Deep Research — Claude Code 商业深度研究 Skill

[English](README.md)

面向 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 的结构化深度研究技能——生成多源验证、标注缺口、框架驱动的商业研究报告。

## 核心问题

LLM 搜索工具给你答案。商业决策需要证据。

快速检索无法告诉你一个市场是否值得进入、竞争对手如何构建护城河、前方有什么监管风险。大多数研究工具产出看似令人信服的浅层摘要，但缺乏严谨性——没有交叉引用、没有缺口标注、没有结构化方法论。

**Business Deep Research 将管理咨询方法论应用到 LLM 驱动的研究中**，产出经得起审查的结构化制品。

## 核心能力

### 五种研究视角，不是一个固定流程

根据问题的形态选择框架——而非一刀切的流水线：

| 研究形态 | 框架 | 产出 |
|---------|------|------|
| 我们是怎么走到这里的？趋势是什么？ | 演化视角 | 历史弧线、拐点、路径依赖 |
| 还有谁在做？壁垒是什么？ | 竞争视角 | 同业地图、护城河分析、定位矩阵 |
| 机会有多大？结构如何？ | 市场视角 | TAM/SAM、价值链、监管版图 |
| 我们该怎么做？有哪些选项？ | 咨询框架 | 议题树、假设检验、建议链 |
| 人们在说什么？有什么规律？ | 研究综合视角 | 主题分析、情感聚类、缺口地图 |

### 多轮检索 + 质量门禁

不是"搜一次就写"。多轮检索，每轮都有显式质量检查：

- **门禁 1**：来源池是否足够支撑所选框架？
- **门禁 2**：证据是否满足框架的前提条件？
- **门禁 3**：综合之前是否显式标注了缺口？

门禁不通过则迭代——精炼查询、扩展范围、或标记局限性。

### 显式缺口标注

每份报告包含结构化的"假设与缺口"章节。不假装知道不知道的事——明确标出缺失信息、不确定项、需要一手调研才能解决的问题。

### 免费工具链，无供应商锁定

基于免费搜索工具设计，无付费 API 依赖。技能自动适配你的 Claude Code 环境中可用的搜索工具。

### 结构化制品，不是聊天文本

产出是结构化文档，不是对话文本：

| 制品 | 用途 |
|------|------|
| **研究简报** | 范围定义——问题、深度配置、约束条件 |
| **搜索日志** | 每个查询、每个来源、包含/排除理由 |
| **研究报告** | 框架驱动的分析，含行内引用 |
| **假设与缺口** | 我们不知道什么、假设了什么、需要验证什么 |

### 中文优先的写作质量

内置 `writing-style-cn.md` 参考文档，确保中文报告读起来自然——不是机器翻译。英文报告遵循同样严谨的结构。

## 安装

```bash
# 项目级安装（推荐——保持研究领域隔离）
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

### 工作流程

1. **确定范围** → 定义问题、选择框架、设定深度配置
2. **搜索** → 多轮检索 + 每阶段质量门禁
3. **分析** → 将选定的视角应用到结构化证据
4. **综合** → 撰写报告，含行内引用和缺口分析
5. **评审** → 按评分标准做质量检查

## 项目结构

```
business-deep-research/
├── SKILL.md                          # Skill 定义
├── agents/openai.yaml                # Agent 配置
├── assets/templates/                 # 4 个结构化输出模板
│   ├── research-brief-template.md    #   研究范围文档
│   ├── search-log-template.md        #   来源审计追踪
│   ├── report-template.md            #   框架驱动报告
│   └── assumptions-and-gaps-template.md  # 缺口分析
├── evals/                            # 评估与质量标准
│   ├── evals.json
│   ├── evaluation-rubric.md
│   └── baseline-pressure-notes.md
├── references/                       # 14 个参考文档
│   ├── framework-selector.md         #   框架路由逻辑
│   ├── competitive-lens.md           #   竞争分析方法论
│   ├── market-lens.md                #   市场结构分析
│   ├── evolution-lens.md             #   历史轨迹分析
│   ├── consulting-problem-solving.md #   假设驱动的问题求解
│   ├── research-synthesis-lens.md    #   定性数据综合
│   ├── search-quality.md             #   来源质量评估
│   ├── strict-verification.md        #   证据验证协议
│   ├── retrieval-rounds.md           #   多轮搜索策略
│   ├── writing-style-cn.md           #   中文写作风格指南
│   └── ...                           #   + 4 个
└── schemas/                          # 4 个 JSON Schema
    ├── source.schema.json            #   来源元数据
    ├── evidence.schema.json          #   证据结构
    ├── claim.schema.json             #   论断结构
    └── run-manifest.schema.json      #   研究运行元数据
```

## 许可证

MIT
