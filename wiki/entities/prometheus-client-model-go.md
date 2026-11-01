---
title: "github.com/prometheus/client_model"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/prometheus-client-model-go-official-research-2026-11-01.md]
---

# github.com/prometheus/client_model

## 用途与适用场景

Prometheus Go 指标数据模型的 protobuf 类型；供 client_golang 等组件交换指标。（[[prometheus-client-model-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/prometheus/client_model`；示例使用 `github.com/prometheus/client_model/go`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[prometheus-project]]：Prometheus 项目组织仓库；个人创建者及维护者名单待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
family := &dto.MetricFamily{}
fmt.Println(family.GetName()) // dto 是该包的常用 import 别名
```

## 关键限制

- 面向 protobuf 数据结构；官方 README 指出历史跨语言用途已收缩，使用时须核对当前暴露格式。

## 来源

- [[prometheus-client-model-go-official-research]]；本地查阅记录：`raw/prometheus-client-model-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/prometheus/client_model)；[Go Packages](https://pkg.go.dev/github.com/prometheus/client_model/go)。
