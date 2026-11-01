---
title: "多实例 P99 聚合示例：原始方案与核对"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, latency, percentile, distributed]
status: growing
sources: [raw/多实例P99例子.md]
author: "未标注（对话摘录）"
source_url: ""
raw_file: "raw/多实例P99例子.md"
format: notes
---

# 多实例 P99 聚合示例：原始方案与核对

## 来源信息

- 作者、原始发表时间和链接未标注；2026-11-01 从 `raw/多实例P99例子.md` 摄入。原文不改。
- 辅助核对：[perks quantile](https://pkg.go.dev/github.com/beorn7/perks/quantile)、[caio/go-tdigest](https://pkg.go.dev/github.com/caio/go-tdigest)、[Prometheus Histograms and summaries](https://prometheus.io/docs/practices/histograms/)；2026-11-01 查阅。

## 一句话概括

> 解释多个 Pod 各有本地延迟分布时，为何不能平均各自的 P99，并比较摘要合并与 Histogram 聚合。

## 核心要点

- 原文第 214–247 行的“局部分位数不能简单平均”是关键结论；全局 P99 定义于所有请求组成的分布，且每个实例的样本量可能不同。
- 原文第 273–310 行提出 Histogram 与可合并摘要两条方向；Prometheus 官方说明 Histogram 可跨实例聚合，客户端预先计算的 quantile 不可直接聚合。

## 与官方文档的冲突

> [!warning] perks.Merge 不可用来求正确的全局 P99
> 原文第 5–7、78–103、183–189、254–271、312–319 行把 `Merge` 描述成“有误差但实例少可用”。[官方 `Stream.Merge` 文档](https://pkg.go.dev/github.com/beorn7/perks/quantile)明确写明该方法已损坏，不能产生正确结果；这不是仅靠减少实例数就能修复的误差。第 79 行只声明 0.99，却在第 90–91 行查询 0.90 和 0.50；官方文档对未预声明的目标分位规定结果未指定。本文不采纳方案 A 的运行结果。

> [!warning] t-digest 示例与所指 Go 包 API 不符
> 原文第 117、147–153、168–170、297–305 行使用 `github.com/caio/go-tdigest`，却调用未在该包文档出现的 `NewWithCompression`。查阅的文档版本使用 `New(tdigest.Compression(100))`，返回 `(*TDigest, error)`；`Add` 和 `Merge` 也返回 error，示例未检查。本文仅保留“可合并摘要”的方案线索，不能把所给代码标为可运行；精度和生产适用性需按数据与版本实测。

- 第 279–288 行给出 Histogram 方向，但经典 Histogram 的跨实例查询须聚合 `_bucket` 时间序列并保留 `le` 标签，例如官方文档的 `histogram_quantile(0.95, sum by (le) (rate(http_request_duration_seconds_bucket[5m])))`。原文写法 `histogram_quantile(0.99, rate(...))` 不足以表达跨 Pod 聚合；若指标单位为 ms，还须让名称、桶边界、SLO 和查询单位一致。
- 本轮未运行原代码，也未验证图示中的 HTTP/gRPC 导出协议；第 94–103 行和图示输出视为说明性文本。

## 与既有知识的关系

- 更新 [[perks-go]] 的 `Merge` 限制，汇入 [[distributed-quantiles]]；与 [[prometheus-client-golang-go]] 的 Histogram 用法相关。

## 由本来源派生 / 更新的页面

- [[distributed-quantiles]]、[[perks-go]]。

## 留给用户的讨论问题

- 目标是观测平台查询跨实例 P99，还是应用内部实时聚合？两者会影响 Histogram 与摘要方案的选型。
