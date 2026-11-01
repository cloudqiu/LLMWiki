---
title: "github.com/xiang90/probing"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/probing-go-official-research-2026-11-01.md]
---

# github.com/xiang90/probing

## 用途与适用场景

通过 HTTP 健康端点持续探测目标，统计丢包和往返时间。（[[probing-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/xiang90/probing`；示例使用 `github.com/xiang90/probing`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- xiang90 仓库归属可核实；个人创建者及当前维护者待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
p := probing.NewProber(http.DefaultTransport)
err := p.AddHTTP("peer", 5*time.Second, []string{"http://localhost:12345/health"})
if err != nil { panic(err) }
```

## 关键限制

- 官方 README 的旧片段与 Go Packages 当前 AddHTTP 签名有差异；按目标版本核对。部署前还需设置对应 HTTP handler。

## 来源

- [[probing-go-official-research]]；本地查阅记录：`raw/probing-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/xiang90/probing)；[Go Packages](https://pkg.go.dev/github.com/xiang90/probing)。
