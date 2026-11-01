---
title: "github.com/ClickHouse/clickhouse-go-linter 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/clickhouse-go-linter-go-official-research-2026-11-01.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://github.com/ClickHouse/clickhouse-go-linter"
raw_file: "raw/clickhouse-go-linter-go-official-research-2026-11-01.md"
format: "official web research notes"
---

# github.com/ClickHouse/clickhouse-go-linter 官方资料查阅

检查 ClickHouse 原生 Go API 中 rows.Err 和 batch.Close 遗漏。 官方模块路径为 `github.com/ClickHouse/clickhouse-go-linter`；收件箱写法为 `github.com/ClickHouse/clickhouse-go-linter`。典型用法见原始研究笔记「安装与用法」。关键限制：仅针对 clickhouse.Open 原生 API，不适用于 database/sql 接口；分析存在跨函数边界限制。

作者与维护：[[clickhouse]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。 资料查阅于 2026-11-01；官方原文未在本地保存，示例未运行。派生库页：[[clickhouse-go-linter-go]]。

## 来源

- [官方资料](https://github.com/ClickHouse/clickhouse-go-linter)；[Go Packages](https://pkg.go.dev/github.com/ClickHouse/clickhouse-go-linter)。
- 本地研究笔记：`raw/clickhouse-go-linter-go-official-research-2026-11-01.md`。
