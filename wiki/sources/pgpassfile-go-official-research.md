---
title: "github.com/jackc/pgpassfile 官方资料查阅"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/pgpassfile-go-official-research-2026-10-31.md]
author: "官方项目文档与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/jackc/pgpassfile"
raw_file: "raw/pgpassfile-go-official-research-2026-10-31.md"
format: "official web research notes"
---

# github.com/jackc/pgpassfile 官方资料查阅

2026-10-31 核对 [Go Packages](https://pkg.go.dev/github.com/jackc/pgpassfile) 与 [官方仓库](https://github.com/jackc/pgpassfile)，摘要为：解析 PostgreSQL .pgpass 密码文件并查找匹配密码。 典型 API 为 `pf, err := pgpassfile.ParsePassfile(strings.NewReader("localhost:5432:db:user:secret\n"))`。关键边界：无匹配时返回空字符串；示例明文仅演示解析，不应写入真实凭据。

作者归属：[[jack-christensen]]：账号仓库，README 称从 pgx 原实现抽出重写。 研究笔记在 `raw/pgpassfile-go-official-research-2026-10-31.md`；本地未保存官方原文副本，示例未运行。派生库页：[[pgpassfile-go]]。
