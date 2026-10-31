---
title: "pgx v5 官方资料查阅记录"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, postgresql, pgx]
status: growing
sources: [raw/pgx-official-research-2026-10-31.md]
author: "jackc/pgx 项目、Go Packages；查阅记录由 Codex 整理"
source_url: "https://github.com/jackc/pgx"
raw_file: raw/pgx-official-research-2026-10-31.md
format: notes
---

# pgx v5 官方资料查阅记录

## 来源信息

- 来源：[pgx 官方仓库](https://github.com/jackc/pgx)、[Go Packages](https://pkg.go.dev/github.com/jackc/pgx/v5)、[v5.12.0 CHANGELOG](https://github.com/jackc/pgx/blob/master/CHANGELOG.md)。
- 查阅日期：2026-10-31；本地文件：`raw/pgx-official-research-2026-10-31.md`。网络代理阻止直接下载，故本地文件是带章节定位的查阅笔记，并非官方原文副本。

## 一句话概括

> pgx v5 是 PostgreSQL 的纯 Go 驱动和工具集，提供原生接口、并发连接池及 `database/sql` 适配器；本次查阅 v5.12.0。

## 核心要点

- 模块路径 `github.com/jackc/pgx/v5`；`Connect` 与 `QueryRow` 可完成单连接查询，跨 goroutine 使用应选 `pgxpool`。（raw 第 1 节）
- v5.12.0 修复两项有特定触发条件的安全问题；实际项目是否受影响须按版本及连接、查询模式核对。（raw 第 2 节）
- [[jack-christensen]] 是 LICENSE 署名者，且近期参与 v5.12.0 标记；完整维护者名单待验证。（raw 第 3–4 节）

## 与既有知识的关系

- 派生 [[pgx-go]] 和 [[jack-christensen]]；作者页记录其他尚未摄入的关联库。
- 未发现与现有 wiki 页的冲突。

## 由本来源派生 / 更新的页面

- [[pgx-go]]
- [[jack-christensen]]
