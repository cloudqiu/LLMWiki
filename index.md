# Index — 知识库目录

> 内容目录（content-oriented）：本库所有页面的清单。每次 ingest 后更新；查询时**先读本文件**找候选页面，再深入具体页面。
> 维护规则见 `CLAUDE.md`。最近更新：2026-10-01。

## Sources 来源

- [[llm-wiki-pattern]] — Karpathy《LLM Wiki》gist：模式原始定义，本库创世文档。2026-10-01 摄入，派生 8 个页面。
- [[as-we-may-think]] — Vannevar Bush《As We May Think》(The Atlantic, 1945-07)：memex 与关联索引的一手文献。2026-10-01 摄入，派生/更新 6 个页面。
- [[claude-code-obsidian-tutorial]] — RUNOOB 中文教程：Claude Code + Obsidian 从零搭建 LLM Wiki；含主题/插件清单与目录结构变体。2026-10-01 摄入，新建 3 页、更新 6 页。

## Concepts 概念

- [[llm-wiki]] — 核心模式：LLM 增量维护的持久化 wiki；三层架构 + ingest/query/lint 三操作。
- [[retrieval-augmented-generation]] — RAG：查询时检索切片生成答案，无知识积累。
- [[memex]] — 桌面式私人「文件与图书馆」(1945)：微缩胶片 + 投影屏 + 关联路径。
- [[associative-trails]] — 关联索引/路径：memex 的核心机制；超链接与交叉引用的思想原点。

## Entities 实体

- [[andrej-karpathy]] — AI 研究者；LLM Wiki 模式作者。（stub）
- [[vannevar-bush]] — OSRD 主任（1945）；memex 构想提出者。
- [[obsidian]] — 本地优先的 markdown 知识管理应用；本库的浏览 IDE。
- [[qmd]] — 本地 markdown 搜索引擎（BM25 + 向量 + LLM 重排）。（stub）
- [[claude-code]] — Anthropic 的终端 agent；本库的维护者（「LLM 是程序员」中的程序员）。
- [[runoob]] — 发布本库首份中文教程来源的公众号。（stub）

## Topics 主题

- [[personal-knowledge-management]] — 个人知识管理：本库正在积累的主题总览（synthesis）。
- [[english-vocabulary]] — 英语词汇系统 hub：收词（inbox）→ 逐词编译（wiki/vocab/en）→ SRS（#flashcards/en）+ 测验复习；含进度与约定。
- [[french-vocabulary]] — 法语词汇系统 hub：收词（raw/vocab-fr-inbox）→ 逐词编译（wiki/vocab/fr）→ SRS（#flashcards/fr）复习；含命名消歧约定。

## Comparisons 对比

- [[llm-wiki-vs-rag]] — 编译式知识 vs. 检索式问答。

## Answers 问答归档

（暂无——有值得留存的查询结果时归档到 `wiki/answers/`）

## Outputs 产物（output/）

- [[2026-10-01-vocab-quiz-01]] — 词汇测验 #1：deplete / off-kilter / unravel（9 题 + 答案解析，2026-10-01）

## Backlog 待建页面

- （建议）Engelbart《Augmenting Human Intellect》(1962)：memex → 人机协同的直接后续
- （建议）超文本谱系：Nelson/Xanadu、H.G. Wells《World Brain》(1938)
- （建议）「预测 vs 实现」对照页：memex 的技术预言哪些成真
- Obsidian Web Clipper 剪藏流程（方法页）
- Marp 幻灯片 / Dataview 查询用法（工具用法页）
- 搜索方案：qmd 集成评估（wiki 规模增长后再做）
- （评估）raw/ 子目录化（articles / papers）——待来源规模增长后再议（output/ 落盘已于 2026-10-01 采纳，见 schema v1.3）

## Stats

- 来源：**3** 份 ｜ wiki 页面：**17** ｜ vocab 词条：**18**（en **17** ｜ fr **1**） ｜ Outputs：**1** ｜ 最近更新：2026-10-01
