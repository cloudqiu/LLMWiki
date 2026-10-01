---
title: 检索增强生成（RAG）
type: concept
created: 2026-10-01
updated: 2026-10-01
tags: [llm, retrieval]
status: growing
sources: [raw/llm-wiki.md]
---

# 检索增强生成（RAG）

## 定义

> 查询时将文档集合切块、检索与问题相关的片段（chunk），交给 LLM 生成答案。NotebookLM、ChatGPT 文件上传与多数 RAG 系统属于此模式。

## 为什么重要 / 解决什么问题

- 让 LLM 基于私有文档作答，无需训练。工程与生态成熟，部署直接，是大规模存量文档问答的常规方案。

## 机制 / 要点（以 Karpathy 的描述为视角）

- 检索发生在**查询时**；知识不沉淀——每个问题都从头重新发现。
- 需要跨文档综合的问题，每次都要重新找到并拼凑相关碎片：**没有积累**。
- 与 [[llm-wiki]] 模式的系统性差异见 [[llm-wiki-vs-rag]]。

## 边界与争议

- 当前页面仅依据 Karpathy 的简述建立；RAG 的完整技术脉络（向量库、切片策略、rerank、混合检索等）待专门来源补充。**待扩展。**
- 两种模式并非互斥：LLM Wiki 规模变大后也可引入检索（[[qmd]]）作为页面定位手段。

## 相关页面

- 对照：[[llm-wiki]]、[[llm-wiki-vs-rag]]
- 来源：[[llm-wiki-pattern]]

## 来源

- raw/llm-wiki.md
