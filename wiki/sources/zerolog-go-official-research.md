---
title: "github.com/rs/zerolog 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/zerolog-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/rs/zerolog"
raw_file: "raw/zerolog-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/rs/zerolog 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/rs/zerolog) 与 [官方仓库](https://github.com/rs/zerolog)，摘要为：链式 API 输出结构化 JSON 日志，适合低分配的服务日志。 典型 API 为 `logger := zerolog.New(os.Stdout).With().Timestamp().Logger()`。关键边界：事件对象短暂复用，不应持有；并发修改 logger context 应遵循文档约束。

作者归属：项目账号 rs；个人创建者姓名与独立维护角色待验证。 研究笔记在 `raw/zerolog-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[zerolog-go]]。
