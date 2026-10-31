---
title: "github.com/jackc/pgpassfile"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/pgpassfile-go-official-research-2026-10-31.md]
---

# github.com/jackc/pgpassfile

## 用途与适用场景

解析 PostgreSQL .pgpass 密码文件并查找匹配密码。（[[pgpassfile-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/jackc/pgpassfile`；示例使用 `github.com/jackc/pgpassfile`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- [[jack-christensen]]：账号仓库，README 称从 pgx 原实现抽出重写。
- 其他相关项目：[tern](https://github.com/jackc/tern)、[pglogrepl](https://github.com/jackc/pglogrepl)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
pf, err := pgpassfile.ParsePassfile(strings.NewReader("localhost:5432:db:user:secret\n"))
if err != nil { log.Fatal(err) }
fmt.Println(pf.FindPassword("localhost", "5432", "db", "user"))
```

## 关键限制

- 无匹配时返回空字符串；示例明文仅演示解析，不应写入真实凭据。

## 来源

- [[pgpassfile-go-official-research]]
- [官方仓库](https://github.com/jackc/pgpassfile)；[Go Packages](https://pkg.go.dev/github.com/jackc/pgpassfile)；[示例 API](https://pkg.go.dev/github.com/jackc/pgpassfile)。
- 本地查阅记录：`raw/pgpassfile-go-official-research-2026-10-31.md`。
