---
title: "github.com/xiang90/probing 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/probing-go-official-research-2026-11-01.md]
author: "官方项目与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/xiang90/probing"
raw_file: "raw/probing-go-official-research-2026-11-01.md"
format: notes
---

# github.com/xiang90/probing 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [Go Packages](https://pkg.go.dev/github.com/xiang90/probing) 和 [官方仓库](https://github.com/xiang90/probing)；研究笔记 `raw/probing-go-official-research-2026-11-01.md` 不是官方原文副本。

## 一句话概括

> 通过 HTTP 健康端点持续探测目标，统计丢包和往返时间。

## 核心要点

- 典型 API：`p := probing.NewProber(http.DefaultTransport)`。（raw「典型 API」）
- 关键边界：官方 README 的旧片段与 Go Packages 当前 AddHTTP 签名有差异；按目标版本核对。部署前还需设置对应 HTTP handler。（raw「关键边界与待验证」）
- 身份证据：xiang90 仓库归属可核实；个人创建者及当前维护者待验证。（raw「创建者、维护者和关联」）

## 与既有知识的关系

- 该模块扩展本库 Go 第三方库索引。
- 创建者或维护范围不能由仓库归属单独推断；未知处已标待验证。

## 由本来源派生 / 更新的页面

- [[probing-go]]。
