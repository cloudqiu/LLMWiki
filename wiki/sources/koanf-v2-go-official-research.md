---
title: "github.com/knadh/koanf/v2 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/koanf-v2-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/knadh/koanf/v2"
raw_file: "raw/koanf-v2-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/knadh/koanf/v2 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/knadh/koanf/v2) 与 [官方仓库](https://github.com/knadh/koanf)，摘要为：从多种 provider 与 parser 加载、合并和读取配置。 典型 API 为 `k := koanf.New(".")`。关键边界：New 只创建空配置；必须 Load 才能读到值。收件箱写作 knadn，官方账号是 knadh。

作者归属：[[kailash-nadh]]：项目原始署名与发布参与；完整维护名单待验证。 研究笔记在 `raw/koanf-v2-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[koanf-v2-go]]。
