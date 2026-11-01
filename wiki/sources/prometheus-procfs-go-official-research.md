---
title: "github.com/prometheus/procfs 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/prometheus-procfs-go-official-research-2026-11-01.md]
author: "官方项目与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/prometheus/procfs"
raw_file: "raw/prometheus-procfs-go-official-research-2026-11-01.md"
format: notes
---

# github.com/prometheus/procfs 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [Go Packages](https://pkg.go.dev/github.com/prometheus/procfs) 和 [官方仓库](https://github.com/prometheus/procfs)；研究笔记 `raw/prometheus-procfs-go-official-research-2026-11-01.md` 不是官方原文副本。

## 一句话概括

> 读取 Linux /proc 的进程和内核统计数据。

## 核心要点

- 典型 API：`fs, err := procfs.NewDefaultFS()`。（raw「典型 API」）
- 关键边界：依赖可用的 Linux procfs；Windows 上不能据此获取本机 /proc 数据。部分旧 New* API 已弃用。（raw「关键边界与待验证」）
- 身份证据：Prometheus 项目组织仓库；个人创建者及维护者名单待验证。（raw「创建者、维护者和关联」）

## 与既有知识的关系

- [[prometheus-client-golang-go]]
- 创建者或维护范围不能由仓库归属单独推断；未知处已标待验证。

## 由本来源派生 / 更新的页面

- [[prometheus-procfs-go]]、[[prometheus-project]]。
