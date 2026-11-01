---
title: "延迟分位数 P50、P90、P99"
type: concept
created: 2026-11-01
updated: 2026-11-01
tags: [latency, percentile, monitoring]
status: growing
sources: [raw/为什么只关心p50 p90 p99.md, raw/单实例模拟P99.md, raw/多实例P99例子.md]
---

# 延迟分位数 P50、P90、P99

## 定义

> 将同一统计窗口内的请求延迟从低到高排列，P50、P90、P99 分别是约 50%、90%、99% 的请求不超过的阈值；具体计算与插值取决于工具和样本数。

## 为什么重要

- 平均值与分位数回答不同问题：平均值反映总和除以次数，分位数描述分布中的位置。只看平均值可能看不见少数慢请求。（[[latency-percentiles-notes]]；raw 第 9–17 行）
- P50 对中心变化敏感，P90/P99 有助于观察较慢请求。选择哪些分位应由服务 SLO、窗口、流量和用户影响决定。（raw 第 19–83 行）

## 机制与要点

- P99 对应阈值，约 1% 的样本仍可能高于它；P99 本身不是“最慢 1% 的平均体验”。
- 三个分位只给出三个位置，不能重建完整分布；最大值、方差、峰型和极端尾部仍可能不同。
- 高分位在低样本数或短窗口中易波动；比较时同时查看请求数、时间窗口与单位。用近似算法时，还须查清误差定义：[[perks-go]] 的 targeted epsilon 是分位位置的绝对误差。（[[single-instance-p99-simulation]]；raw 第 31–50、136–143 行）

## 边界与争议

> [!warning] 原始说明的夸大表述
> [[latency-percentiles-notes]] 所据 raw 第 7、79 行称三个点足以构成完整画像；第 89 行考试成绩类比方向不一致。原文保留，但本页不沿用这两个结论。

- 单实例模拟采用 90% 的 10–50ms 和 10% 的 100–300ms（raw `单实例模拟P99.md` 第 65–73 行）；若按理想均匀混合分布推算，P99 约为 280ms，不能把原文约 200ms 的示意输出视为确定预期。

## 相关页面

- [[single-instance-p99-simulation]]、[[distributed-quantiles]]、[[multi-instance-p99-examples]]、[[perks-go]]。

## 来源

- `raw/为什么只关心p50 p90 p99.md` 第 1–101 行；`raw/单实例模拟P99.md` 第 1–159 行；`raw/多实例P99例子.md` 第 214–319 行。
- 辅助核对：[perks quantile 包文档](https://pkg.go.dev/github.com/beorn7/perks/quantile)。
