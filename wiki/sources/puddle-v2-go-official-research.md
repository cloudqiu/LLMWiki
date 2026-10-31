---
title: "github.com/jackc/puddle/v2 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/puddle-v2-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/jackc/puddle/v2"
raw_file: "raw/puddle-v2-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/jackc/puddle/v2 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/jackc/puddle/v2) 与 [官方仓库](https://github.com/jackc/puddle)，摘要为：以泛型提供最小化的并发资源池。 典型 API 为 `pool, err := puddle.NewPool(&puddle.Config[int]{`。关键边界：Acquire 可阻塞，须传可取消 context；Release 后不得继续使用 Resource；Close 等待资源归还。

作者归属：[[jack-christensen]]：账号下的 pgx 家族资源池仓库；具体共同维护者待验证。 研究笔记在 `raw/puddle-v2-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[puddle-v2-go]]。
