---
title: "github.com/prometheus/client_golang"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/prometheus-client-golang-go-official-research-2026-11-01.md, raw/多实例P99例子.md]
---

# github.com/prometheus/client_golang

## 用途与适用场景

在 Go 服务中创建和收集 Prometheus 指标。（[[prometheus-client-golang-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/prometheus/client_golang`；示例使用 `github.com/prometheus/client_golang/prometheus`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[prometheus-project]]：Prometheus 项目组织仓库；未将组织归属推断为个人作者。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
requests := prometheus.NewCounter(prometheus.CounterOpts{Name: "requests_total", Help: "Requests."})
prometheus.MustRegister(requests)
requests.Inc()
```

## 关键限制

- 注册同名指标会失败；label 基数应控制。模块根路径包含多个包，此例使用 prometheus 子包。
- 跨实例求全局延迟分位时，应使用可聚合的 Histogram 桶并按官方查询格式聚合；本页的 Counter 示例不处理延迟分布。详见 [[distributed-quantiles]]（`raw/多实例P99例子.md` 第 273–290 行的方案及其中的查询缺口）。

## 来源

- [[prometheus-client-golang-go-official-research]]；本地查阅记录：`raw/prometheus-client-golang-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/prometheus/client_golang)；[Go Packages](https://pkg.go.dev/github.com/prometheus/client_golang/prometheus)。
