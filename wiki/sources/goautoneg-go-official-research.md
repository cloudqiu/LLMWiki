---
title: "github.com/munnerz/goautoneg 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/goautoneg-go-official-research-2026-11-01.md]
author: "官方项目与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/munnerz/goautoneg"
raw_file: "raw/goautoneg-go-official-research-2026-11-01.md"
format: notes
---

# github.com/munnerz/goautoneg 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [Go Packages](https://pkg.go.dev/github.com/munnerz/goautoneg) 和 [官方仓库](https://github.com/munnerz/goautoneg)；研究笔记 `raw/goautoneg-go-official-research-2026-11-01.md` 不是官方原文副本。

## 一句话概括

> 根据 HTTP Accept 请求头从候选媒体类型中选择响应 Content-Type。

## 核心要点

- 典型 API：`choice := goautoneg.Negotiate("application/json, text/plain;q=0.5", []string{"text/plain", "application/json"})`。（raw「典型 API」）
- 关键边界：仓库自称原 bitbucket.org/ww/goautoneg 的镜像；镜像账号不等于原创作者，原始创建者与现维护者待验证。（raw「关键边界与待验证」）
- 身份证据：镜像仓库 README 署名 Open Knowledge Foundation Ltd. 版权；个人创建者待验证。（raw「创建者、维护者和关联」）

## 与既有知识的关系

- 该模块扩展本库 Go 第三方库索引。
- 创建者或维护范围不能由仓库归属单独推断；未知处已标待验证。

## 由本来源派生 / 更新的页面

- [[goautoneg-go]]。
