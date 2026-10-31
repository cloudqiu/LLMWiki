---
title: "koanf TOML parser v2 官方资料查阅记录"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, koanf, toml, config]
status: growing
sources: [raw/koanf-toml-v2-official-research-2026-10-31.md]
author: "knadh/koanf 项目、Go Packages；查阅记录由 Codex 整理"
source_url: "https://pkg.go.dev/github.com/knadh/koanf/parsers/toml/v2"
raw_file: raw/koanf-toml-v2-official-research-2026-10-31.md
format: notes
---

# koanf TOML parser v2 官方资料查阅记录

## 来源信息

- 来源：[parser 的 Go Packages 文档](https://pkg.go.dev/github.com/knadh/koanf/parsers/toml/v2)、[v2.2.2 源码](https://github.com/knadh/koanf/blob/parsers/toml/v2.2.2/parsers/toml/toml.go)、[koanf 官方 README](https://github.com/knadh/koanf)。
- 查阅日期：2026-10-31；本地文件：`raw/koanf-toml-v2-official-research-2026-10-31.md`。本地文件是查阅笔记，并非官方原文副本。

## 一句话概括

> `parsers/toml/v2` 为 koanf 提供独立安装的 TOML 格式解析器，解析能力来自 `go-toml/v2`。

## 核心要点

- 本次查阅版本 v2.2.2；入口 `toml.Parser()`，可用于 `koanf.Load` 的 parser 参数。（raw 第 1 节）
- koanf 的核心、provider 与 parser 是分别安装的模块；该 parser 本身不读取文件或环境变量。（raw 第 1 节）
- [[kailash-nadh]] 是 koanf LICENSE 署名者和近期 release 发布参与者；parser 子模块的独立作者及完整维护者名单尚待验证。（raw 第 2–3 节）

## 与既有知识的关系

- 派生 [[koanf-toml-v2-go]] 与 [[kailash-nadh]]；其他 koanf 模块还在收件箱中，未因本次查阅而自动摄入。
- 未发现与现有 wiki 页的冲突。

## 由本来源派生 / 更新的页面

- [[koanf-toml-v2-go]]
- [[kailash-nadh]]
