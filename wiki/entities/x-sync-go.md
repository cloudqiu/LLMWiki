---
title: "golang.org/x/sync"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/x-sync-go-official-research-2026-11-01.md]
---

# golang.org/x/sync

## 用途与适用场景

补充 Go 并发原语；errgroup 汇聚 goroutine 错误并传播取消。（[[x-sync-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get golang.org/x/sync`；示例使用 `golang.org/x/sync/errgroup`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- Go 项目维护的 x 仓库；个人创建者及当前维护者名单待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
g, ctx := errgroup.WithContext(context.Background())
_ = ctx
g.Go(func() error { return nil })
if err := g.Wait(); err != nil { panic(err) }
```

## 关键限制

- errgroup 的派生 Context 在首个错误或 Wait 返回时取消；同一 Group 不应重复用于不同任务。

## 来源

- [[x-sync-go-official-research]]；本地查阅记录：`raw/x-sync-go-official-research-2026-11-01.md`。
- [官方仓库](https://go.googlesource.com/sync)；[Go Packages](https://pkg.go.dev/golang.org/x/sync/errgroup)。
