---
title: LLM Wiki 模式
type: concept
created: 2026-10-01
updated: 2026-10-01
tags: [knowledge-management, llm, pattern]
status: growing
sources: [raw/llm-wiki.md, raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md]
---

# LLM Wiki 模式

## 定义

> 由 LLM 增量构建并持续维护的持久化 markdown wiki：位于用户与原始资料之间的知识编译层。知识**编译一次、持续保鲜**，而非每次查询重新检索推导。

## 为什么重要 / 解决什么问题

- 传统 RAG 每次查询都从原始文档重新检索、拼凑，**没有积累**——一个需要跨 5 篇文档综合的细微问题，每次都要从头再发现一遍（→ [[retrieval-augmented-generation]]）。
- LLM Wiki 把综合工作前移并沉淀：交叉引用建好、矛盾标注好、综述始终反映已读的全部内容。**wiki 是持久、可复利的产物**（→ [[llm-wiki-vs-rag]]）。
- 维护知识库的真正负担是记账（交叉引用、保持摘要最新、一致性维护），而非阅读或思考。人类因维护成本随规模膨胀而放弃；LLM 不会无聊、一遍可改 15 个文件，维护成本趋近于零。

## 机制 / 要点

### 三层架构

1. **原始资料层**（本库 `raw/`）：精选资料，**不可变**，source of truth。
2. **wiki 层**（本库 `wiki/`）：LLM 全权拥有——创建页面、随新资料更新、维护交叉引用、保持一致性。用户读，LLM 写。
3. **schema 层**（本库 `CLAUDE.md`）：结构与工作流约定，使 LLM 成为「有纪律的 wiki 维护者」而非普通聊天机器人；由用户与 LLM 共同演进。

### 三个操作

- **Ingest 摄入**：读资料 → 与用户讨论要点 → 写摘要页 → 更新相关实体/概念页（可能 10-15 页）→ 更新 index → 追加 log。
- **Query 查询**：先读 index 找页 → 读页 → 带引用作答；**好答案回填成新的 wiki 页面**，让探索也复利。
- **Lint 巡检**：查矛盾、过时论断、孤立页、缺页概念、缺失交叉引用、可搜索补齐的数据缺口。

### 分工

- 用户：策划来源、引导分析、提好问题、理解含义。
- LLM：「其余全部」（summarizing, cross-referencing, filing, bookkeeping）。
- 实践形态：agent 与 Obsidian 分屏；「Obsidian 是 IDE；LLM 是程序员；wiki 是代码库」。

## 边界与争议

- **规模上限**：index.md 模式在约 100 份来源 / 数百页内有效，更大时需引入搜索（[[qmd]]）。
- **质量风险**：LLM 维护的一致性需要人类抽查；来源未展开错误传播问题。本库的缓解手段：lint 巡检 + 矛盾在两处显式标注（见 `CLAUDE.md` §3.3、§5）。
- **抽象性**：原文是 idea file，结构、约定、工具皆为示例；「一切可选、模块化」，应随实际需求裁剪（本库即一次实例化）。
- **实例化空间**：社区实践已出现结构变体——RUNOOB 教程（[[claude-code-obsidian-tutorial]]）用 `raw/` 子目录（articles / papers）、`wiki/synthesis/` 与 `output/`；本库则 `raw/` 平铺 + wiki 六类目录。gist 明言结构示例性，两种并存成立。

## 相关页面

- 来源：[[llm-wiki-pattern]]；中文教程：[[claude-code-obsidian-tutorial]]
- 对照：[[llm-wiki-vs-rag]]、[[retrieval-augmented-generation]]
- 思想前身：[[memex]]（[[vannevar-bush]]）与其中的 [[associative-trails|关联路径]] 机制——「连接与文档本身同等重要」
- 工具：[[obsidian]]、[[qmd]]
- 主题：[[personal-knowledge-management]]

## 来源

- raw/llm-wiki.md（Karpathy, "LLM Wiki" gist）
- raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md（RUNOOB 教程：转述与实例化）
