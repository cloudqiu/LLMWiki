---
title: "github.com/prometheus/client_golang 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/prometheus-client-golang-go-official-research-2026-11-01.md]
author: "官方项目与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/prometheus/client_golang/prometheus"
raw_file: "raw/prometheus-client-golang-go-official-research-2026-11-01.md"
format: notes
---

# github.com/prometheus/client_golang 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [Go Packages](https://pkg.go.dev/github.com/prometheus/client_golang/prometheus) 和 [官方仓库](https://github.com/prometheus/client_golang)；研究笔记 `raw/prometheus-client-golang-go-official-research-2026-11-01.md` 不是官方原文副本。

## 一句话概括

> 在 Go 服务中创建和收集 Prometheus 指标。

## 核心要点

- 典型 API：`requests := prometheus.NewCounter(prometheus.CounterOpts{Name: "requests_total", Help: "Requests."})`。（raw「典型 API」）
- 关键边界：注册同名指标会失败；label 基数应控制。模块根路径包含多个包，此例使用 prometheus 子包。（raw「关键边界与待验证」）
- 身份证据：Prometheus 项目组织仓库；未将组织归属推断为个人作者。（raw「创建者、维护者和关联」）

## 与既有知识的关系

- [[prometheus-client-model-go]]、[[prometheus-common-go]]
- 创建者或维护范围不能由仓库归属单独推断；未知处已标待验证。

## 由本来源派生 / 更新的页面

- [[prometheus-client-golang-go]]、[[prometheus-project]]。
