---
title: "golang.org/x/time"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/x-time-go-official-research-2026-11-01.md]
---

# golang.org/x/time

## 用途与适用场景

提供时间相关辅助包；rate 用 token bucket 限制事件速率。（[[x-time-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get golang.org/x/time`；示例使用 `golang.org/x/time/rate`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- Go 项目维护的 x 仓库；个人创建者及当前维护者名单待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
lim := rate.NewLimiter(rate.Limit(2), 4)
fmt.Println(lim.Allow())
```

## 关键限制

- rate 按每秒速率和 burst 计数；Allow 会丢弃超额请求，需等待时改用 Wait(ctx)。

## 来源

- [[x-time-go-official-research]]；本地查阅记录：`raw/x-time-go-official-research-2026-11-01.md`。
- [官方仓库](https://go.googlesource.com/time)；[Go Packages](https://pkg.go.dev/golang.org/x/time/rate)。
