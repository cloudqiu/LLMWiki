---
title: "github.com/munnerz/goautoneg"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/goautoneg-go-official-research-2026-11-01.md]
---

# github.com/munnerz/goautoneg

## 用途与适用场景

根据 HTTP Accept 请求头从候选媒体类型中选择响应 Content-Type。（[[goautoneg-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/munnerz/goautoneg`；示例使用 `github.com/munnerz/goautoneg`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- 镜像仓库 README 署名 Open Knowledge Foundation Ltd. 版权；个人创建者待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
choice := goautoneg.Negotiate("application/json, text/plain;q=0.5", []string{"text/plain", "application/json"})
fmt.Println(choice)
```

## 关键限制

- 仓库自称原 bitbucket.org/ww/goautoneg 的镜像；镜像账号不等于原创作者，原始创建者与现维护者待验证。

## 来源

- [[goautoneg-go-official-research]]；本地查阅记录：`raw/goautoneg-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/munnerz/goautoneg)；[Go Packages](https://pkg.go.dev/github.com/munnerz/goautoneg)。
