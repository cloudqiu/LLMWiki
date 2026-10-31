# pgx v5 官方资料查阅记录（2026-10-31）

本文件是 Codex 阅读官方页面后的定位笔记，**不是官方网页原文快照**。本机网络代理阻止了直接下载；事实和引用请回到下列链接核对。收件箱条目仅用于确定待查库。

## 1. 项目、版本与用法

- 官方仓库及 README：https://github.com/jackc/pgx 。「Quick Start」说明 `pgx` 是 PostgreSQL 的纯 Go 驱动和工具集，安装 `go get github.com/jackc/pgx/v5`。示例用 `pgx.Connect(ctx, os.Getenv("DATABASE_URL"))` 建连接，再用 `QueryRow(ctx, sql, args...).Scan(...)` 读取一行。
- Go Packages：https://pkg.go.dev/github.com/jackc/pgx/v5 。2026-10-31 查阅时显示 v5.12.0；只对本次查阅版本作说明，不断言以后仍为最新版。
- README「Documentation」「Choosing Between the pgx and database/sql Interfaces」：`pgxpool` 为并发安全的连接池；`stdlib` 是 `database/sql` 适配器。直接 pgx 接口适合仅使用 PostgreSQL 且不依赖 `database/sql` 的项目，支持 `LISTEN`/`NOTIFY`、`COPY` 等 PostgreSQL 特性。
- Go Packages「Conn」：单个 `*pgx.Conn` **不支持并发使用**；多个 goroutine 共享数据库访问应使用连接池。
- Go Packages「PgBouncer」：默认的命名 prepared statements 在 PgBouncer 1.21+ 且 `max_prepared_statements>0` 的相应池化模式中可用；较旧版本或禁用该功能时，文档建议 `QueryExecModeExec`。本文不将其写成所有 PgBouncer 配置都需要改动。
- README「Supported Go and PostgreSQL Versions」在查阅时写 Go 1.25+、PostgreSQL 14+；支持窗口会随上游版本变动，不作为长期固定承诺。

## 2. v5.12.0 更新与限制

- 官方 CHANGELOG：https://github.com/jackc/pgx/blob/master/CHANGELOG.md ，「5.12.0 (October 30, 2026)」。该版本修复两项高严重度、触发条件较窄的安全问题，官方建议受影响应用升级至 v5.12.0。
- 第一项：v5.12.0 之前，`SendBatch` 使用**非默认** simple protocol 时，在特定 `--` 注释与攻击者可控字符串参数组合下可引发 SQL 注入；默认 extended protocol 不受该项影响。公告：GHSA-j38q-h3ph-jjpq。
- 第二项：v5.9.0–v5.11.0 在依赖 `require_auth` 或 `channel_binding=require` 且没有 `sslmode=verify-full` 等服务器身份验证时，可能接受伪装服务器绕过认证；v5.12.0 已修复。公告：GHSA-95fj-3fxw-g62g。此问题不能绕过 TLS 服务器证书验证。
- v5.12.0 还为 `BatchResults` 接口增加 `Tx` 方法；自定义实现和 mock 可能需要更新。

## 3. 作者与其他库

- pgx 官方 LICENSE：https://github.com/jackc/pgx/blob/master/LICENSE ，版权行署名 Jack Christensen（2013–2021）；个人主页 https://github.com/jackc 将 `pgx` 和 `tern` 置顶，确认账号名称与本人姓名。
- v5.12.0 官方 tag：https://github.com/jackc/pgx/releases/tag/v5.12.0 ，`jackc` 账号于 2026-10-31 标记该版本。这能确认 Jack 在当日仍参与版本发布；不据此推断他是唯一维护者。
- pgx README「PGX Family Libraries」列出 [pglogrepl](https://github.com/jackc/pglogrepl)（逻辑复制客户端）、[tern](https://github.com/jackc/tern)（SQL 迁移工具）、[pgerrcode](https://github.com/jackc/pgerrcode)（PostgreSQL 错误码常量）等 Jack 账号下的关联项目。它们尚未摄入，且该列表不证明 Jack 独立编写了每个库；其中 `pgerrcode` 已在 Go 收件箱待摄入。

## 4. 待验证

- 用户项目的 pgx 与 PostgreSQL 版本、是否使用 PgBouncer 或受上述安全公告影响；示例未在本机运行。
- 项目的完整当前维护者名单；可证实 Jack 近期发布参与，但不声称唯一维护。
