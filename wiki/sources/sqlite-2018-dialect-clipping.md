---
title: "SQLite 2018 SQL 特性转载（剪藏标题与正文不符）"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [sqlite, sql, source-criticism]
status: growing
sources: ["raw/微信为什么使用 SQLite 保存聊天记录？.md"]
author: "原文 Markus Winand；剪藏转载账号小哈学Java"
source_url: "https://mp.weixin.qq.com/s/genD-1mZyrm27CVwW76wtw"
raw_file: "raw/微信为什么使用 SQLite 保存聊天记录？.md"
format: "article"
---

# SQLite 2018 SQL 特性转载

## 来源信息

- 本地文件：`raw/微信为什么使用 SQLite 保存聊天记录？.md`。剪藏标题问“微信为什么使用 SQLite 保存聊天记录”，但正文 19–209 行实为 Markus Winand [《SQLite in 2018》](https://modern-sql.com/blog/2019-01/sqlite-in-2018) 的中文转载，未给出微信使用 SQLite 的实现证据。
- 剪藏页来源链接指向[微信公众号](https://mp.weixin.qq.com/s/genD-1mZyrm27CVwW76wtw)；原文发表于 2019-01。剪藏 frontmatter 的 2026-10-07 是创建日期，非原文发表日期。

## 一句话概括

文章回顾 SQLite 3.22.0–3.26.0 左右的布尔表达式、窗口函数、`FILTER`、UPSERT 与重命名列能力，是 **2018 年的版本快照**。

## 核心要点

- 布尔值及 `IS NOT FALSE` 与 `<> FALSE` 对 NULL 的处理不同；原文 38–75 行。
- 窗口函数在 3.25.0 引入；原文 84–113 行；[SQLite 官方窗口函数文档](https://www.sqlite.org/windowfunctions.html)。
- `INSERT ... SELECT ... ON CONFLICT` 的解析歧义可用 `WHERE true` 消除；原文 146–177 行；[SQLite 官方 UPSERT 文档](https://www.sqlite.org/lang_upsert.html)。

> [!warning] 矛盾：2018 年快照与现行 SQLite
> 原文 140 行说 `FILTER` 只能用于窗口聚合，不能用于普通 `GROUP BY` 聚合。这对应当时的版本范围；SQLite 3.30.0（2019-10-04）已加入普通聚合的 `FILTER` 支持，见[官方发布说明](https://www.sqlite.org/releaselog/3_30_0.html)。相关结论也在 [[sqlite-filter-clause]] 标注。

## 与既有知识的关系

- 派生 [[sqlite-filter-clause]]；用作 SQL 功能演进资料，不用作微信聊天存储证据。
- 图片仍为远程链接，且对比表反映 2018 年环境；当前数据库横向比较须重新核对版本。

## 留给用户的讨论问题

- 若仍关注微信本地存储机制，需要指定平台和版本，并另找可审计的一手资料。
