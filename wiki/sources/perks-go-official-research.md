---
title: "github.com/beorn7/perks 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/perks-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/beorn7/perks"
raw_file: "raw/perks-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/beorn7/perks 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/beorn7/perks) 与 [官方仓库](https://github.com/beorn7/perks)，摘要为：提供流式近似分位数 quantile 等 Go 工具包。 典型 API 为 `q := quantile.NewTargeted(map[float64]float64{0.9: 0.01})`。关键边界：根模块不是 quantile 包；Stream 文档称非线程安全。原始 README 版权署名 Blake Mizerany，当前 beorn7 仓库维护角色待验证。

作者归属：原始 README 版权署名 Blake Mizerany；beorn7 的个人身份与当前维护角色待验证。 研究笔记在 `raw/perks-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[perks-go]]。
