---
title: "pgx v5 (Go)"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, postgresql, pgx, database]
status: growing
sources: [raw/pgx-official-research-2026-10-31.md]
---

# pgx v5

## 用途与适用场景

pgx 是 PostgreSQL 的纯 Go 驱动及工具集。仅使用 PostgreSQL、需要 `COPY` 或 `LISTEN`/`NOTIFY` 等特性时可用原生 pgx 接口；需要标准 `database/sql` 的库时可用其 `stdlib` 适配器。并发访问可用 `pgxpool`。（[[pgx-official-research]]；raw 第 1 节）

## 依赖与版本

- 语言 / 生态：Go、PostgreSQL；模块路径 `github.com/jackc/pgx/v5`。
- 查阅版本 / 日期：Go Packages 显示 v5.12.0；2026-10-31。用户项目版本待验证。
- 在 Go 模块项目中执行 `go get github.com/jackc/pgx/v5`；运行查询需要可访问的 PostgreSQL 实例和连接串。官方 README 查阅时说明支持 Go 1.25+ 与 PostgreSQL 14+，该支持窗口会变化。（raw 第 1 节）

## 作者与维护者

- 创建者 / 原始版权署名：[[jack-christensen]]；项目 LICENSE 署名 Jack Christensen。（raw 第 3 节）
- 当前维护参与：[[jack-christensen]] 于 2026-10-31 标记 v5.12.0；完整维护者名单待验证，不将其写作唯一维护者。（raw 第 3–4 节）

## 典型用法

在已安装依赖、设置 `DATABASE_URL` 且 PostgreSQL 可连接的目录中保存为 `main.go` 并运行 `go run .`。查询 `select 1` 不要求预建表。此例依据官方 `Connect`、`QueryRow` 和 `Scan` 用法编写，**尚未实际运行**。（raw 第 1 节）

```go
package main

import (
    "context"
    "fmt"
    "log"
    "os"

    "github.com/jackc/pgx/v5"
)

func main() {
    ctx := context.Background()
    conn, err := pgx.Connect(ctx, os.Getenv("DATABASE_URL"))
    if err != nil {
        log.Fatal(err)
    }
    defer conn.Close(ctx)

    var n int
    if err := conn.QueryRow(ctx, "select 1").Scan(&n); err != nil {
        log.Fatal(err)
    }
    fmt.Println(n)
}
```

## 关键限制

- 单个 `*pgx.Conn` 不能由多个 goroutine 并发使用；服务中的共享数据库访问应使用 `pgxpool`。（raw 第 1 节）
- 使用较旧 PgBouncer 或禁用 prepared statements 时，需按官方文档选择兼容的 `QueryExecMode`；默认配置在支持 prepared statements 的 PgBouncer 1.21+ 场景可用。（raw 第 1 节）
- 官方 v5.12.0 修复了两项高严重度问题：**非默认 simple-protocol `SendBatch`** 的特定 SQL 注入情形，以及 **v5.9.0–v5.11.0** 在特定认证配置下接受伪装服务器的情形。受影响项目应按 [官方变更记录](https://github.com/jackc/pgx/blob/master/CHANGELOG.md) 核对并升级；不把所有旧版本或默认查询都概括为同样风险。（raw 第 2 节）
- 若自行实现 `BatchResults` 接口，升级至 v5.12.0 时需核对新增 `Tx` 方法。（raw 第 2 节）

## 来源

- [[pgx-official-research]]
- [官方仓库与 README](https://github.com/jackc/pgx)
- [Go Packages 文档](https://pkg.go.dev/github.com/jackc/pgx/v5)
- [v5.12.0 CHANGELOG](https://github.com/jackc/pgx/blob/master/CHANGELOG.md)
- 本地查阅记录：`raw/pgx-official-research-2026-10-31.md`
