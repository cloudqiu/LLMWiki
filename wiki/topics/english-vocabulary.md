---
title: 英语词汇（Vocabulary）
type: topic
created: 2026-10-01
updated: 2026-10-01
tags: [vocabulary, english, learning]
status: growing
sources: [raw/vocab-inbox.md]
---

# 英语词汇（Vocabulary）

## 概述

本库的英语词汇管理系统（2026-10-01 建立）。分工：

> `raw/vocab-inbox.md` 收词（用户）→ `wiki/vocab/` 逐词编译与富化（LLM）→ 词族 / 易混 / 主题综合（持续）→ 复习双轨：SRS 插件排程 + Claude 按需出题。

词条富化含：IPA、词性、双语释义、例句（含翻译）、词根/词族、同义/搭配、易混提示；不确定信息标「待验证」。阅读词条本身即为第一遍复习；`learning` 字段（new → learning → known）跟踪掌握度。

## 进度

- 词条：**0**（new 0 ｜ learning 0 ｜ known 0）；更新于 2026-10-01
- 待处理：inbox 中暂无积压

## 怎么用

1. **收词**：把生词追加到 `raw/vocab-inbox.md`（一行一个，可附来源/例句）；或在会话中口述「这批词：…」——Claude 先**原样**记入 `raw/vocab-capture-YYYY-MM-DD.md` 再编译。
2. **编译**：说「ingest vocab」→ 去重、逐词建/更新词条（每批 20-50 词）、更新本页、记 log。
3. **复习**：SRS 插件每日刷卡（扫描范围含 `wiki/vocab`）；想测验就说「考我：最近 20 个 new 词」→ Claude 出题（cloze / 翻译 / 辨析），产物落 `output/`。

## 结构约定

- 词条路径：`wiki/vocab/<word>.md`（小写 lemma；**不逐条进 index.md**）
- 标签：`src/<来源>`（如 src/reading、src/书名-slug，标注在哪读到的）、`domain/<领域>`（如 domain/tech、domain/finance，工作/专业领域）——按需取用
- 闪卡：词条内 `word:::释义`（Spaced Repetition 插件兼容；`:::` = 双向卡）
- 插件扫描范围：`wiki/vocab`

## 词族 / 综合页

（暂无——出现值得综合的词族、易混对或主题簇时在此登记，并链到对应页面）

## 开放问题

- **SRS 插件选型（待装）**：Spaced Repetition（经典，生态兼容最广，卡片语法即本库所用）vs LearnKit / EngramQuest（FSRS 新算法）vs 语言学习专用（English Vocabulary Learning Plugin、Klomimory）。选定后在此记录配置。
- 例句来源：当前为 LLM 生成 + 待验证标记；是否引入词典核对流程？
- Dataview（未装）：装上后本页可改为动态统计表（按 learning / tags 查询）。

## 来源

- raw/vocab-inbox.md（收词入口）
- 系统设计：2026-10-01 query 会话（决策记录见 `log.md`）
