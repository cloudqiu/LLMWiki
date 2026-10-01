---
title: LLM Wiki vs RAG
type: comparison
created: 2026-10-01
updated: 2026-10-01
tags: [knowledge-management, llm, retrieval]
status: growing
sources: [raw/llm-wiki.md, raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md]
---

# LLM Wiki vs RAG

## 结论摘要

> RAG 在**查询时**检索原始切片、即用即弃；LLM Wiki 在**摄入时**把知识编译进持久互联的页面、持续维护。前者适合大规模存量文档的一次性问答，后者适合长期累积、需要综合与追踪观点演变的个人/团队知识库。

## 对比

| 维度 | RAG | LLM Wiki |
| --- | --- | --- |
| 知识处理时机 | 查询时检索 chunks | 摄入时编译进 wiki，查询时读已编译页面 |
| 积累性 | 无——每个问题从头发现 | 有——交叉引用、矛盾标注、综述持续沉淀：「复利资产」 |
| 跨文档综合 | 每次重新拼凑（如综合 5 篇） | 综合已写入概念/主题页，直接可读 |
| 矛盾处理 | 每次查询临时面对 | 摄入时即显式标注、留痕 |
| 基础设施 | 向量库 / 嵌入 / 检索服务 | markdown 目录 + `index.md`（约 100 份来源内够用） |
| 维护者 | 无人（无状态） | LLM 全权维护；人只策展与提问 |
| 答案追溯 | 检索到的片段 | 页面交叉引用 + 回指 raw 原文 |
| 规模特性 | 随文档量扩展较好 | 中等规模（~百份来源/数百页）表现好，更大需加搜索（[[qmd]]） |

## 适用场景

- 选 RAG：海量存量文档、无法预先策展、需要服务化/多租户的一次性问答。
- 选 LLM Wiki：长期知识累积、需要综合与观点演变追踪、愿意「策展 + 对话」的深度使用者（研究、读书、个人追踪、团队内部 wiki）。
- 两者可叠加：wiki 规模变大后在 wiki 层上做检索（[[qmd]]），而非回到原始文档层。

## 相关页面

- [[llm-wiki]]、[[retrieval-augmented-generation]]、[[llm-wiki-pattern]]

## 来源

- raw/llm-wiki.md（对比维度提炼自原文 "The core idea"、"Indexing and logging"、"Optional: CLI tools" 各节）
- raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md（RUNOOB 教程对同一对比的复述，见其 L22）
