---
title: "chi v5 (Go)"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, chi, http, router]
status: growing
sources: [raw/chi-official-research-2026-10-31.md]
---

# chi v5

## 用途与适用场景

chi 是轻量、可组合的 Go HTTP 路由库，用于按路径和方法分发请求，并用 middleware、路由组或子路由组织 API。它与标准库 `net/http` handler 兼容，适合需要在 Go 服务中明确组织多个 REST 风格端点的场景。（[[chi-official-research]]；raw 第 1 节）

## 依赖与版本

- 生态：Go `net/http`；模块路径 `github.com/go-chi/chi/v5`。
- 查阅版本 / 日期：Go Packages 的 v5.5.0，2026-10-31；用户本地版本待验证。
- 在 Go 模块项目中安装：`go get github.com/go-chi/chi/v5`。官方资料称核心库无外部依赖。（raw 第 1 节）

## 作者与维护者

- 作者：[[peter-kieltyka]]；官方 README 版权行和本人自述支持其作者身份。（raw 第 1–2 节）
- 当前维护者：**待验证**。仓库归属 `go-chi` 组织，但这不足以确认个人或团队的当前维护角色。（raw 第 3 节）

## 典型用法

在已执行 `go mod init` 和上述 `go get` 的目录中保存为 `main.go`，运行 `go run .`，然后访问 `/users/42`。这是依据官方 `NewRouter`、`Get`、`URLParam` API 组成的最小示例；**尚未实际运行**。（raw 第 1 节）

```go
package main

import (
    "fmt"
    "log"
    "net/http"

    "github.com/go-chi/chi/v5"
)

func main() {
    r := chi.NewRouter()
    r.Get("/users/{id}", func(w http.ResponseWriter, req *http.Request) {
        fmt.Fprint(w, chi.URLParam(req, "id"))
    })
    log.Fatal(http.ListenAndServe(":3000", r))
}
```

## 关键限制

- 路由路径须以 `/` 开头；有无结尾 `/` 是不同匹配情形，须按预期设置。（raw 第 1 节「URL patterns」）
- 若需获取客户端 IP，不要直接沿用已废弃的 `middleware.RealIP`；应按可信代理拓扑选择官方 `ClientIPFrom*` middleware。（raw 第 1 节「Choosing a ClientIP middleware」）
- 用户项目的 Go 版本与 chi 版本尚未核对；官方文档的支持范围表述为“最近四个 Go 主版本”，本文不固定最低版本号。（raw 第 1 节）

## 来源

- [[chi-official-research]]
- [官方仓库](https://github.com/go-chi/chi)
- [Go Packages 文档（查阅时显示 v5.5.0）](https://pkg.go.dev/github.com/go-chi/chi/v5)
- 本地查阅记录：`raw/chi-official-research-2026-10-31.md`
