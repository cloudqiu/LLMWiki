---
title: "github.com/knadh/koanf/providers/rawbytes 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/koanf-rawbytes-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/knadh/koanf/providers/rawbytes"
raw_file: "raw/koanf-rawbytes-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/knadh/koanf/providers/rawbytes 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/knadh/koanf/providers/rawbytes) 与 [官方仓库](https://github.com/knadh/koanf)，摘要为：把内存中的 []byte 作为 koanf 配置源；常与 JSON、TOML 等 parser 配合。 典型 API 为 `k := koanf.New(".")`。关键边界：只提供原始字节，不负责解析格式；需要另配 parser。收件箱写作 rawybytes，官方路径为 rawbytes。

作者归属：[[kailash-nadh]]：koanf 项目原始署名；子模块的独立作者待验证。 研究笔记在 `raw/koanf-rawbytes-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[koanf-rawbytes-go]]。
