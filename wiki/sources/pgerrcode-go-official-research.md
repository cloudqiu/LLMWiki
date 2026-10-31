---
title: "github.com/jackc/pgerrcode 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/pgerrcode-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/jackc/pgerrcode"
raw_file: "raw/pgerrcode-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/jackc/pgerrcode 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/jackc/pgerrcode) 与 [官方仓库](https://github.com/jackc/pgerrcode)，摘要为：给 PostgreSQL SQLSTATE 错误码提供命名常量。 典型 API 为 `fmt.Println(pgerrcode.UniqueViolation == "23505")`。关键边界：本库只提供常量；要识别真实数据库错误，需与驱动返回的 SQLSTATE 配合。

作者归属：[[jack-christensen]]：账号下的 pgx 家族仓库；个人具体提交贡献需查 git 历史。 研究笔记在 `raw/pgerrcode-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[pgerrcode-go]]。
