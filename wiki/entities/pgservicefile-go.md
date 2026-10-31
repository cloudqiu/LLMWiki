---
title: "github.com/jackc/pgservicefile"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/pgservicefile-go-official-research-2026-10-31.md]
---

# github.com/jackc/pgservicefile

## 用途与适用场景

解析 PostgreSQL .pg_service.conf 服务配置。（[[pgservicefile-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/jackc/pgservicefile`；示例使用 `github.com/jackc/pgservicefile`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- [[jack-christensen]]：账号下的 pgx 家族仓库；个人具体提交贡献待验证。
- 其他相关项目：[tern](https://github.com/jackc/tern)、[pglogrepl](https://github.com/jackc/pglogrepl)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
sf, err := pgservicefile.ParseServicefile(strings.NewReader("[local]\nhost=localhost\n"))
if err != nil { log.Fatal(err) }
svc, err := sf.GetService("local")
fmt.Println(svc.Settings["host"], err)
```

## 关键限制

- 服务不存在会返回错误；旧 pkg.go.dev 页面显示伪版本，具体依赖版本以 go.mod 锁定。

## 来源

- [[pgservicefile-go-official-research]]
- [官方仓库](https://github.com/jackc/pgservicefile)；[Go Packages](https://pkg.go.dev/github.com/jackc/pgservicefile)；[示例 API](https://pkg.go.dev/github.com/jackc/pgservicefile)。
- 本地查阅记录：`raw/pgservicefile-go-official-research-2026-10-31.md`。
