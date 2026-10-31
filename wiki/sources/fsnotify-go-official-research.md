---
title: "github.com/fsnotify/fsnotify 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/fsnotify-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/fsnotify/fsnotify"
raw_file: "raw/fsnotify-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/fsnotify/fsnotify 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/fsnotify/fsnotify) 与 [官方仓库](https://github.com/fsnotify/fsnotify)，摘要为：跨平台文件系统变更通知。 典型 API 为 `w, err := fsnotify.NewWatcher()`。关键边界：必须持续读取 Events 与 Errors；操作系统与文件系统可能丢事件，目录监控通常比单文件监控稳妥。

作者归属：fsnotify 社区组织；个人创建者和当前维护者待验证。 研究笔记在 `raw/fsnotify-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[fsnotify-go]]。
