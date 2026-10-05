# 美赛论文固定章节写作 Skill

用于 MCM/ICM、HiMCM/MidMCM 论文的前置章节及文末模型优缺点，依据赛题、已有论文和指定模板撰写或修改内容。沿用调用名 `mcm-front-matter-writing`。

本项目记录个人写作规范，不是赛事官方要求。具体版式服从指定赛事、年份、模板及用户当前要求。

## 章节结构

```text
1 Introduction
  1.1 Problem Background
  1.2 Problem Restatement and Analysis
  1.3 Our Work
2 Assumptions and Justification
3 Notations
... 模型建立、求解、检验等正文 ...
N Strengths and Weaknesses
  N.1 Strengths
  N.2 Weaknesses
```

`N` 随全文自动编号。完整论文中的模型优缺点位于模型正文之后；仅测试固定章节时可按需要接在当前文档末尾。

## 核心要求

- **语言风格**：平实、专业、严谨、学术化，用词冷静克制。使用领域认可的术语，避免生造词、夸张修辞、宣传性评价和缺乏依据的结论。不滥用 `not ... but ...`、`rather than`、引号、冒号、破折号或增补式解释。
- **Problem Background**：只写一段，交代研究对象、现实问题、影响和建模必要性，不提前介绍算法或计算结果。
- **Problem Restatement and Analysis**：按加粗的 `Task 1:`、`Task 2:` 等列出可执行任务，每项只保留完成什么、考虑什么、交付什么。
- **Our Work**：仅保留空白图框、图题和引用标签。后续图画好后，在原位置插入成图。
- **Assumptions and Justification**：最多四条。首行加粗假设，下一行以加粗的 `Justification:` 开始说明理由；每条总计不超过目标版式中的三行。
- **Notations**：使用 `Symbol`、`Description`、`Unit` 三列的标准三线表，无竖线或逐行横线，表后不加说明段、脚注或总结。
- **Strengths and Weaknesses**：分别列出优点与缺点，每点以加粗短标题接简洁说明，含标题最多两行。优点写具体设计及作用，缺点写限制、影响和对应改进方向，评价须有论文依据。

假设的三行限制和模型优缺点的两行限制均按目标模板实际排版核查。示例的符号数量、图框尺寸及三优三缺的条数不构成通用限制；不要通过缩小字号、行距或页边距来满足篇幅要求。

## 文件

```text
skills/mcm-front-matter-writing/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── latex-layout.md
    └── evacuation-example.md
```

- [SKILL.md](skills/mcm-front-matter-writing/SKILL.md)：范围、语言风格、各章节规则与交付检查。
- [LaTeX 格式与检查](skills/mcm-front-matter-writing/references/latex-layout.md)：空图占位、假设块、三线表、模型优缺点列表及实际行数检查。
- [疏散论文写法对照](skills/mcm-front-matter-writing/references/evacuation-example.md)：以 2025 HiMCM A、Team 16390 论文为依据的改写片段，用于展示写法，不是原论文逐字摘录。

## 使用

将 `skills/mcm-front-matter-writing` 文件夹放入本地 Codex 的 skills 目录，默认位置为 `~/.codex/skills/`。调用示例：

```text
使用 $mcm-front-matter-writing，依据这份赛题和论文撰写前置章节与文末模型优缺点。
沿用当前英文 LaTeX 文档，保持平实、严谨、克制的语言风格。
Our Work 仅留空图占位；假设最多四条，每条含理由不超过三行；
Notations 使用标准三线表，表后不加说明。
优缺点分别列项，每点含加粗短标题最多两行，保留具体作用或局限及改进方向。
```

也可以只要求其中一个小节。已有 LaTeX 文档时在原文件内修改并检查编译；结构校验通过不能替代目标文档的行数和分页核查。

摘要写作可配合独立的 [mcm-summary-writing](https://github.com/ranranrannervous/MathModeling-LLM-Prompts/tree/main/skills/mcm-summary-writing) 使用。本 skill 的范围不包括摘要正文、模型正文或 Our Work 绘图。
