---
title: "github.com/go-viper/mapstructure/v2 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/mapstructure-v2-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/go-viper/mapstructure/v2"
raw_file: "raw/mapstructure-v2-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/go-viper/mapstructure/v2 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/go-viper/mapstructure/v2) 与 [官方仓库](https://github.com/go-viper/mapstructure)，摘要为：将 map 解码到 Go struct，常用于配置处理。 典型 API 为 `var cfg struct { Port int `mapstructure:"port"` }`。关键边界：默认 Decode 不等于输入校验；未知字段要配置 ErrorUnused。v2 为 go-viper 分支，勿与原 v1 混用。

作者归属：go-viper 社区维护分支；个人创建及维护角色待验证。 研究笔记在 `raw/mapstructure-v2-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[mapstructure-v2-go]]。
