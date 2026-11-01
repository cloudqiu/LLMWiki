---
title: "github.com/pelletier/go-toml/v2 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/go-toml-v2-go-official-research-2026-11-01.md]
author: "官方项目与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/github.com/pelletier/go-toml/v2"
raw_file: "raw/go-toml-v2-go-official-research-2026-11-01.md"
format: notes
---

# github.com/pelletier/go-toml/v2 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [Go Packages](https://pkg.go.dev/github.com/pelletier/go-toml/v2) 和 [官方仓库](https://github.com/pelletier/go-toml)；研究笔记 `raw/go-toml-v2-go-official-research-2026-11-01.md` 不是官方原文副本。

## 一句话概括

> 把 TOML 文本解码为 Go 结构，也可将结构编码为 TOML。

## 核心要点

- 典型 API：`var cfg struct { Name string `toml:"name"` }`。（raw「典型 API」）
- 关键边界：收件箱 pelleiter 为拼写错误；官方模块路径为 pelletier。TOML v2 与 v1 是不同导入路径。（raw「关键边界与待验证」）
- 身份证据：Thomas Pelletier 的官方 GitHub 主页将 go-toml 列为项目；具体版本维护者名单待验证。（raw「创建者、维护者和关联」）

## 与既有知识的关系

- [[koanf-toml-v2-go]]
- 创建者或维护范围不能由仓库归属单独推断；未知处已标待验证。

## 由本来源派生 / 更新的页面

- [[go-toml-v2-go]]、[[thomas-pelletier]]。
