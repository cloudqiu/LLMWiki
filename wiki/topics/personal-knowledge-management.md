---
title: 个人知识管理（PKM）
type: topic
created: 2026-10-01
updated: 2026-10-01
tags: [knowledge-management]
status: growing
sources: [raw/llm-wiki.md, raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md]
---

# 个人知识管理（PKM）

## 概述

本库正在积累的主题：**个人如何长期积累、组织与调取知识**。当前核心论点（来自唯一来源）：真正的瓶颈不是阅读与思考，而是**维护（记账）**；把维护交给 LLM 后，知识库可以像代码库一样持续集成，知识得以复利（[[llm-wiki]]）。

## 脉络

- **1945** — Vannevar Bush 发表《[[as-we-may-think]]》(The Atlantic)：提出 [[memex]]——桌面式私人「文件与图书馆」（微缩胶片 + 投影屏）；核心机制是 [[associative-trails|关联索引]]：连接任意两项成「路径」，可巡游、可分享；预言「trail blazers」新职业。**未解决**：路径的构建与维护仍靠用户本人。
- **检索时代** — RAG / NotebookLM 等：查询时检索，无积累（[[retrieval-augmented-generation]]）。
- **现在** — [[llm-wiki]]：LLM 充当维护者，知识编译一次、持续保鲜；人只做策展与提问。
- **传播期** — 模式进入中文社区教学（[[claude-code-obsidian-tutorial]]，RUNOOB）并出现多种结构实例化；本库与之同期落地。

## 页面地图

| 页面 | 类型 | 一句话 |
| --- | --- | --- |
| [[llm-wiki]] | 概念 | 核心模式：LLM 维护的持久化 wiki |
| [[llm-wiki-vs-rag]] | 对比 | 编译式知识 vs. 检索式问答 |
| [[retrieval-augmented-generation]] | 概念 | 查询时检索的传统路径 |
| [[memex]] | 概念 | 桌面式私人知识设备 (1945) |
| [[associative-trails]] | 概念 | 关联索引/路径：memex 的核心机制 |
| [[as-we-may-think]] | 来源 | Bush 1945 原文（memex 一手文献） |
| [[vannevar-bush]] | 实体 | memex 提出者（OSRD 主任） |
| [[llm-wiki-pattern]] | 来源 | Karpathy 原文（本库创世文档） |
| [[obsidian]] | 实体 | 人与 wiki 之间的界面 |
| [[andrej-karpathy]] | 实体 | 模式作者 |
| [[claude-code-obsidian-tutorial]] | 来源 | 中文教程：从零搭建（含结构变体） |
| [[claude-code]] | 实体 | 执行维护的 agent（本库维护者） |
| [[runoob]] | 实体 | 教程发布者（stub） |

## 开放问题

- LLM 维护 wiki 的质量如何审计？（本库目前靠 lint 巡检 + 矛盾显式标注；是否足够？）
- 规模上限的实证：100 份来源之后，`index.md` 模式是否仍够用？何时需要 [[qmd]]？
- 与「间隔重复 / 主动回忆」等记忆方法如何结合？——**已落地并迁出**：英/法双语词汇系统 2026-10-01 建立、同日整体迁出为独立词汇库 LLMLangWiki（SRS 插件 + Claude 出题双轨），本库不再承载词汇；效果待观察。
- 谱系线：memex → Engelbart (1962) → 超文本（Nelson）→ wiki 反向链接，这条演变线如何逐段深化？
- 与团队协作场景如何衔接（多人 + LLM 共同维护）？
- 目录结构收敛：本库约定（raw 平铺 + 六类 wiki 目录）与教程变体（raw 子目录 / synthesis / output）保持并存，还是收敛其一？

## 来源

- raw/llm-wiki.md
- raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md
