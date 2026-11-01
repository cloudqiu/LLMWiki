---
title: "跨实例延迟分位数聚合"
type: concept
created: 2026-11-01
updated: 2026-11-01
tags: [latency, percentile, distributed, prometheus]
status: growing
sources: [raw/多实例P99例子.md, raw/单实例模拟P99.md]
---

# 跨实例延迟分位数聚合

## 定义

> 全局分位数来自所有实例在同一时间窗口内的请求延迟总体；单独算出的各实例 P99 不能再平均为全局 P99。

## 为什么重要

实例请求量、流量组合、长尾形状可能不同。即便三个 Pod 的本地 P99 已知，也无法仅凭这些值重建总体第 99 百分位。（[[multi-instance-p99-examples]]；raw 第 214–247 行）

## 机制与要点

- 小规模、离线且允许传输原始观测值时，可合并原始样本求精确分位；大规模在线观测通常需要可聚合表示。
- Prometheus 官方文档区分可跨实例聚合的 Histogram 与预先在客户端计算、不能直接聚合的 quantile。经典 Histogram 查询须对 `_bucket` 在实例间求和并保留 `le`，再调用 `histogram_quantile`；精度受桶边界限制。[[prometheus-client-golang-go]] 提供 Histogram 类型。（raw 第 273–290 行；[官方文档](https://prometheus.io/docs/practices/histograms/)）
- 可合并摘要（如 t-digest）是另一种思路；其具体 Go API、误差、序列化协议和资源成本均需按选择的实现验证。（raw 第 105–179、293–310 行）

## 边界与争议

> [!warning] perks Merge 的原文建议与官方文档冲突
> [[multi-instance-p99-examples]] 所据 raw 第 5–7、78–103、183–189、254–271、312–319 行称少量实例可用 `quantile.Stream.Merge`。官方包文档明确标注该方法损坏且不能产生正确结果，因此本页不将它列为可用的全局 P99 方案。[[perks-go]] 也同步标注。

> [!warning] 原文 t-digest 代码不可直接使用
> raw 第 117、147–153、168–170 行调用 `NewWithCompression`，但所指 [caio/go-tdigest 文档](https://pkg.go.dev/github.com/caio/go-tdigest)使用 `New(tdigest.Compression(...))` 并返回 error；`Add`、`Merge` 也返回 error。仅保留架构思路，实际实现待验证。

## 相关页面

- [[latency-percentiles]]、[[multi-instance-p99-examples]]、[[perks-go]]、[[prometheus-client-golang-go]]。

## 来源

- `raw/多实例P99例子.md` 第 1–321 行；`raw/单实例模拟P99.md` 第 25–57 行。
- 辅助核对：[perks quantile](https://pkg.go.dev/github.com/beorn7/perks/quantile)、[caio/go-tdigest](https://pkg.go.dev/github.com/caio/go-tdigest)、[Prometheus Histograms and summaries](https://prometheus.io/docs/practices/histograms/)。
