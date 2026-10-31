---
title: "github.com/coreos/go-semver 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/go-semver-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/coreos/go-semver"
raw_file: "raw/go-semver-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/coreos/go-semver 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/coreos/go-semver) 与 [官方仓库](https://github.com/coreos/go-semver)，摘要为：解析和比较 SemVer 版本号。 典型 API 为 `v, err := semver.NewVersion("1.2.3")`。关键边界：根仓库含命令；在 Go 代码中导入 /semver 子包。对前导 v、范围表达式的支持需按文档核对。

作者归属：coreos 组织仓库；个人作者与当前维护角色待验证。 研究笔记在 `raw/go-semver-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[go-semver-go]]。
