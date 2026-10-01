---
title: "LLM Wiki: A pattern for building personal knowledge bases using LLMs"
type: source
created: 2026-10-01
updated: 2026-10-01
tags: [knowledge-management, llm, pattern]
status: mature
author: Andrej Karpathy
source_url: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
raw_file: raw/llm-wiki.md
format: idea-document
---

# LLM Wiki: A pattern for building personal knowledge bases using LLMs

## 来源信息

- 作者：[[andrej-karpathy]]
- 形式：idea file——刻意抽象的模式说明，设计为直接粘贴给 LLM agent（Codex、Claude Code、OpenCode/Pi 等），由 agent 与用户共同实例化出具体实现
- 本地文件：`raw/llm-wiki.md`（下载于 2026-10-01）
- 原始链接：https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

## 一句话概括

> 让 LLM 增量构建并维护一个持久、互联的 markdown wiki（位于用户与原始资料之间），把知识「编译一次、持续保鲜」，替代每次查询都重新检索拼凑的 RAG 模式。

## 核心要点

- 与 RAG 的本质区别：RAG 每次查询从头检索重组、**没有积累**；LLM Wiki 把知识沉淀为持久产物——交叉引用已建好、矛盾已标注、综述已反映全部已读内容（→ [[llm-wiki-vs-rag]]）。原话：**「wiki 是持久、可复利的产物」（a persistent, compounding artifact）**。
- 三层架构：**原始资料**（不可变，source of truth）/ **wiki**（LLM 全权拥有与维护）/ **schema**（如 CLAUDE.md，用户与 LLM 共同演进）→ [[llm-wiki]]。
- 三个操作：**ingest** 摄入（一份资料可能触及 10-15 个页面）、**query** 查询（好答案回填成新页面）、**lint** 巡检（矛盾、过时论断、孤立页、缺页概念、缺失交叉引用、可搜索补齐的数据缺口）。
- 两个导航文件：`index.md`（内容目录，查询先读它；约 100 份来源 / 数百页内足够，无需向量检索基建）与 `log.md`（追加式时间线，固定前缀便于 grep）。
- 实践形态：LLM agent 与 Obsidian 分屏——「**Obsidian 是 IDE；LLM 是程序员；wiki 是代码库**」。
- 为什么成立：知识库的苦役是记账（bookkeeping）而非阅读思考；人类因维护负担增长快过价值而放弃 wiki，LLM「不会无聊，一遍可触及 15 个文件」，维护成本趋近于零。
- 思想前身：Vannevar Bush 1945 年的 [[memex]] 构想——Bush 没能解决「谁来维护」，LLM 恰好补上（→ [[vannevar-bush]]）。
- 应用场景：个人追踪（目标/健康/心理/日志）、研究深潜、逐章读书（做自己的 Tolkien Gateway 式伴读 wiki）、团队/业务内部 wiki（Slack、会议记录、人工审查兜底）、竞品分析、尽调、旅行规划、课程笔记、爱好深潜。

## 关键细节

- 原文对「个人使用」的建议：**一次摄入一份、保持参与**（读摘要、检查更新、引导重点）；批量摄入也可以，但监督更少。工作流应写进 schema 供后续会话沿用。
- 目录结构、schema 约定、页面格式、工具**全部是示例性的**：原文明确「一切可选、模块化」，应由 agent 与用户按需实例化。**本库即一次实例化**，具体约定见根目录 `CLAUDE.md`。
- 查询的输出形式多样：markdown 页 / 对比表 / Marp 幻灯片 / matplotlib 图表 / canvas。
- 可选工具：[[qmd]]（本地 markdown 混合搜索 + LLM 重排，有 CLI 与 MCP）；Obsidian Web Clipper 剪藏文章；图片下载到本地（附件目录设为 `raw/assets/`）；graph view 看结构；Marp 做幻灯片；Dataview 查 frontmatter；wiki 作为 git 仓库获得版本历史。
- 图片注意：LLM 无法一次性阅读含内嵌图片的 markdown——先读文本，再单独查看引用的图片。

## 与既有知识的关系

- 本资料是**本库的创世文档**：目录结构、页面类型、工作流与约定均由此实例化而来（见 `CLAUDE.md`、`log.md` 的 setup 条目）。
- 与 RAG / NotebookLM / ChatGPT 文件上传等「检索式」做法形成对照 → [[retrieval-augmented-generation]]、[[llm-wiki-vs-rag]]。
- 后续实践：中文社区已据本 gist 写成从零搭建教程（[[claude-code-obsidian-tutorial]]，RUNOOB）——本库与该教程是同一模式的两次独立实例化。

## 由本来源派生 / 更新的页面

- 来源摘要：本页
- 概念：[[llm-wiki]]、[[retrieval-augmented-generation]]、[[memex]]
- 实体：[[andrej-karpathy]]、[[obsidian]]、[[qmd]]
- 对比：[[llm-wiki-vs-rag]]
- 主题：[[personal-knowledge-management]]

## 留给用户的讨论问题

- 你的主要摄入场景是哪一类（研究 / 读书 / 个人追踪 / 工作）？据此调整页面类型与模板。
- 摄入节奏：保持默认的「一次一份、边聊边摄入」，还是某些主题批量摄入？
- 是否启用 `git init`？是否在规模增长后配置 qmd 搜索？
