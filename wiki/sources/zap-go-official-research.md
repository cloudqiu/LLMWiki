---
title: "go.uber.org/zap 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/zap-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/go.uber.org/zap"
raw_file: "raw/zap-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# go.uber.org/zap 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/go.uber.org/zap) 与 [官方仓库](https://github.com/uber-go/zap)，摘要为：Uber Go 的结构化日志库，以强类型字段记录日志。 典型 API 为 `logger, err := zap.NewProduction()`。关键边界：NewProduction 默认 JSON 输出；Sync 在部分输出设备上可返回不影响日志的错误，按运行环境处理。

作者归属：uber-go 项目组织；个人创建者与当前维护名单待验证。 研究笔记在 `raw/zap-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[zap-go]]。
