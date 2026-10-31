---
title: "github.com/cespare/xxhash/v2 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/xxhash-v2-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/cespare/xxhash/v2"
raw_file: "raw/xxhash-v2-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/cespare/xxhash/v2 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/cespare/xxhash/v2) 与 [官方仓库](https://github.com/cespare/xxhash)，摘要为：计算快速的 XXH64 非密码学哈希。 典型 API 为 `sum := xxhash.Sum64String("hello")`。关键边界：不能用于密码、签名或抗攻击散列；v2 import 路径必须带 /v2。

作者归属：仓库账号 cespare；个人姓名及完整维护角色待验证。 研究笔记在 `raw/xxhash-v2-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[xxhash-v2-go]]。
