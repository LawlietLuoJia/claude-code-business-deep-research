# Business Deep Research — Claude Code 商业深度研究 Skill

[English](README.md)

面向 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 的结构化深度研究技能——生成多源验证、标注缺口、框架驱动的商业研究报告。

适用于商业尽调、竞品分析、市场研究、决策备忘录等需要深度调研的场景。

## 功能特性

- **框架驱动分析**：5 种研究视角（演化、竞争、市场、咨询问题求解、研究综合）
- **多源验证**：交叉引用证据，严格引用要求
- **搜索质量门禁**：每个研究阶段内置质量检查
- **中英双语输出**：支持中英文报告撰写
- **制品化输出**：结构化产出——研究简报、搜索日志、研究报告、假设与缺口
- **免费工具链**：基于免费搜索工具设计，无付费 API 依赖

## 安装

将本目录复制到 Claude Code skills 目录：

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
```

```
deep research / competitive research / market analysis / business decision memo
```

### 工作流程

1. **确定范围** → 定义研究问题、深度配置、交付物
2. **搜索** → 多轮检索 + 质量门禁
3. **分析** → 应用框架视角处理结构化证据
4. **综合** → 撰写带引用、缺口和影响的报告
5. **评审** → 按评分标准做质量检查

### 研究视角

| 研究形态 | 主视角 | 参考文档 |
|---------|--------|---------|
| 起源、演化、历史决策、现状定位 | 演化视角 | `references/evolution-lens.md` |
| 同业比较、护城河、定位 | 竞争视角 | `references/competitive-lens.md` |
| 市场定义、机会、行业结构、监管、风险 | 市场视角 | `references/market-lens.md` |
| 商业问题、选项、建议链 | 咨询框架 | `references/consulting-problem-solving.md` |
| 访谈、问卷、工单、反馈、定性主题 | 研究综合视角 | `references/research-synthesis-lens.md` |

## 项目结构

```
business-deep-research/
├── SKILL.md                     # Skill 定义
├── agents/
│   └── openai.yaml              # OpenAI 兼容 agent 配置
├── assets/
│   └── templates/               # 输出模板
│       ├── assumptions-and-gaps-template.md   # 假设与缺口
│       ├── report-template.md                 # 报告模板
│       ├── research-brief-template.md         # 研究简报
│       └── search-log-template.md             # 搜索日志
├── evals/                       # 评估与质量标准
│   ├── baseline-pressure-notes.md
│   ├── evals.json
│   └── evaluation-rubric.md
├── references/                  # Skill 参考文档（14个）
│   ├── competitive-lens.md      # 竞争分析视角
│   ├── consulting-problem-solving.md  # 咨询问题求解
│   ├── depth-profile.md         # 深度配置
│   ├── evolution-lens.md        # 演化视角
│   ├── framework-selector.md    # 框架选择器
│   ├── long-report.md           # 长报告格式
│   ├── market-lens.md           # 市场视角
│   ├── output-contract.md       # 输出契约
│   ├── research-synthesis-lens.md  # 研究综合视角
│   ├── retrieval-rounds.md      # 检索轮次策略
│   ├── runtime-adapters.md      # 运行时适配器
│   ├── search-quality.md        # 搜索质量标准
│   ├── strict-verification.md   # 严格验证规则
│   └── writing-style-cn.md      # 中文写作风格
└── schemas/                     # JSON Schema（4个）
    ├── claim.schema.json        # 论断结构
    ├── evidence.schema.json     # 证据结构
    ├── run-manifest.schema.json # 运行清单
    └── source.schema.json       # 来源结构
```

## 许可证

MIT
