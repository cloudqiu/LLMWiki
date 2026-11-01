# github.com/ClickHouse/clickhouse-go-linter 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/ClickHouse/clickhouse-go-linter`。
- 核对模块：`github.com/ClickHouse/clickhouse-go-linter`。
- [项目官方资料](https://github.com/ClickHouse/clickhouse-go-linter)；[Go Packages](https://pkg.go.dev/github.com/ClickHouse/clickhouse-go-linter)。
- 用途：检查 ClickHouse 原生 Go API 中 rows.Err 和 batch.Close 遗漏。

## 安装与用法

```sh
go install github.com/ClickHouse/clickhouse-go-linter@latest
```

```text
clickhouse-go-linter ./...
```

## 身份与限制

- [[clickhouse]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。
- 仅针对 clickhouse.Open 原生 API，不适用于 database/sql 接口；分析存在跨函数边界限制。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。

## 身份与其他项目证据

- [官方个人或组织主页](https://github.com/ClickHouse)核对账号身份。
- [同账号或组织的其他项目](https://github.com/ClickHouse/ch-go)；仅作待摄入线索，个人创建者/维护者角色待验证。
