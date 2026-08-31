---
name: insigoo-wiki
version: 2.0.0
description: LLM Wiki 基础版 — 零依赖的知识库体系。只需文件夹+Markdown索引，任何组织都能拥有AI可检索的知识库。
author: insigoo (因思阁)
license: MIT
trigger_keywords: [知识库, wiki, 建索引, 整理知识, 知识管理, 目录索引]
---

# insigoo Wiki — 知识库基础版

> 零依赖。一个文件夹 + 四个索引文件 = AI 能检索的知识库。
>
> 升级路线：Wiki版(本包) → RAG版(insigoo-knowledge-base) → SAG版(insigoo-sag)

---

## 四级索引体系

```
knowledge_index.md    — 目录索引: 文件在哪个区、最后更新日期
project_index.md      — 项目索引: 文件属于哪个项目/主题
scenario_index.md     — 场景索引: 你能问什么来找到这个文件
corpus_index.md       — 语料索引: Agent从对话中提炼的问答路径 [v2.0]
```

---

## 知识库结构

```bash
你的文件夹/
├── knowledge_index.md         ← ① 总索引（自动维护）
├── project_index.md           ← ② 项目索引
├── scenario_index.md          ← ③ 场景索引
├── corpus_index.md            ← ④ 语料索引
├── 📰 资讯/
├── 📚 学习/
├── 🎨 物料/
├── 📝 方案/
├── 🏃 记录/
├── 💰 财务/
├── 📊 评估/
├── 📦 归档/
└── 🏢 行政/
```

> 如果你使用 [insigoo-memory](https://github.com/ericyueric/insigoo-memory)（SAG 知识库架构师方法论），可参考其建库流程，在 Agent 协助下建立并维护这些目录。

---

## 四级索引详解

### ① 目录索引 (knowledge_index.md)

自动生成。记录每个文件属于哪个区域 + 最后更新日期。

```markdown
# knowledge_index

## 📰 资讯
- 政策通知_2026.md (2026-03-01)
- 合作协议_ABC公司.md (2026-01-15)

## 📝 方案
- Q2产品规划.md (2026-02-20)
- 市场推广方案_v2.md (2026-04-10)
```

### ② 项目索引 (project_index.md)

按项目/主题关联文件。一个文件可以属于多个项目。

```markdown
# project_index

## 市场推广项目
- 📝 方案: 市场推广方案_v2.md
- 🏃 记录: 202604_推广活动记录.md
- 💰 财务: Q1预算执行表.xlsx
- 📊 评估: 推广效果评估报告.md

## 产品规划
- 📝 方案: Q2产品规划.md
- 🏃 记录: 用户访谈纪要.csv
```

### ③ 场景索引 (scenario_index.md)

按"你能问什么"来索引。这是最贴近用户使用的索引。

```markdown
# scenario_index

## 场景: 员工入职
- 入职流程 → 行政/入职指南.md
- 合同模板 → 行政/劳动合同模板.docx
- 常见问题: 社保怎么办理 → 行政/社保办理流程.md

## 场景: 财务管理
- 预算怎么做 → 财务/预算模板.xlsx
- 报销流程 → 行政/报销制度.md
```

### ④ 语料索引 (corpus_index.md) [v2.0]

Agent 从对话中自动提炼的"问答路径"。高频问答无需重复搜索。

```markdown
# corpus_index

| 用户问 | Agent找到 | 频次 | 最后使用 |
|--------|----------|:--:|---------|
| 合同模板在哪 | 行政/劳动合同模板.docx | 5 | 2026-06-15 |
| Q1花了多少钱 | 财务/Q1预算执行表.xlsx | 3 | 2026-06-10 |
| 怎么写周报 | 归档/周报模板_2025.md | 8 | 2026-06-20 |
```

**自动维护规则**：
- Agent 每次成功回答一条知识库问题，语料索引 +1
- 超过 30 天未使用的语料自动归档
- 频次 ≥ 5 的语料标记为 🔥 热路径，Agent 优先从语料库匹配

---

## 维护

参考 [insigoo-memory](https://github.com/ericyueric/insigoo-memory) 的索引健康检查流程，定期核验：断链 / 空区 / 重复文件 / 过时文件 / 语料频次异常。

---

## 升级路径

| 版本 | 适用文件量 | 搜索方式 | 需要 |
|------|:---:|------|------|
| **Wiki 版** (本包) | 10-50 | 文件名+目录 | 零依赖 |
| **RAG 版** | 50-500 | 语义向量搜索 | + Ollama |
| **SAG 版** | 500+ | Agent MCP 搜索 | + Docker |

---

*insigoo 因思阁 · insigoo@insigoo.cn · github.com/ericyueric/insigoo-wiki*
