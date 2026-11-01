---
title: "github.com/prometheus/common"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/prometheus-common-go-official-research-2026-11-01.md]
---

# github.com/prometheus/common

## 用途与适用场景

Prometheus 组件共享的 Go 包；expfmt 处理指标文本与格式协商。（[[prometheus-common-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/prometheus/common`；示例使用 `github.com/prometheus/common/expfmt`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[prometheus-project]]：Prometheus 项目组织仓库；个人创建者及维护者名单待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
format := expfmt.ResponseFormat(http.Header{})
fmt.Println(format)
```

## 关键限制

- 模块根路径不是单一 API；expfmt 的不同版本存在已弃用 API，需查目标版本。

## 来源

- [[prometheus-common-go-official-research]]；本地查阅记录：`raw/prometheus-common-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/prometheus/common)；[Go Packages](https://pkg.go.dev/github.com/prometheus/common/expfmt)。
