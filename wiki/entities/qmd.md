---
title: qmd
type: entity
entity_type: tool
created: 2026-10-01
updated: 2026-10-01
tags: [tool, search]
status: stub
sources: [raw/llm-wiki.md]
---

# qmd

## 简介

tobi/qmd：面向 markdown 文件的**本地搜索引擎**（仓库：https://github.com/tobi/qmd）。混合 BM25 / 向量检索 + LLM 重排，全部在本机运行。

## 关键事实

- 同时提供 CLI（LLM 可直接 shell 调用）与 MCP server（作为原生工具接入 agent）。
- 定位：wiki 规模超出 `index.md` 管理能力后的搜索层；小规模不需要。

## 在本库中的角色

- 候选工具（见 `index.md` Backlog）：本库当前规模远未需要，待页面数量增长后评估。

## 相关页面

- [[llm-wiki]]、[[obsidian]]

## 来源

- raw/llm-wiki.md（原文 "Optional: CLI tools" 一节）
