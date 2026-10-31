---
title: "google/uuid 官方资料查阅记录"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, uuid]
status: growing
sources: [raw/google-uuid-official-research-2026-10-31.md]
author: "google/uuid 项目、Go Packages；查阅记录由 Codex 整理"
source_url: "https://github.com/google/uuid"
raw_file: raw/google-uuid-official-research-2026-10-31.md
format: notes
---

# google/uuid 官方资料查阅记录

## 来源信息

- 来源：[官方仓库与 README](https://github.com/google/uuid)、[Go Packages](https://pkg.go.dev/github.com/google/uuid)、[CONTRIBUTORS](https://github.com/google/uuid/blob/master/CONTRIBUTORS)。
- 查阅日期：2026-10-31；本地文件：`raw/google-uuid-official-research-2026-10-31.md`。网络代理阻止直接下载，故本地文件是带章节定位的查阅笔记，并非官方原文副本。

## 一句话概括

> `google/uuid` 提供 Go 的 UUID 生成、解析与检查 API；其实现源自更早的 `pborman/uuid`，但两者类型和接口不能混为一谈。

## 核心要点

- 模块路径 `github.com/google/uuid`；本次查阅 Go Packages 显示 v1.6.0。`UUID` 是 16 字节数组。（raw 第 1 节）
- `NewRandom` 可生成随机 v4 UUID 并返回错误；`Parse` 接受多种格式，不能用作只接受标准形式的校验。（raw 第 1 节）
- [[paul-borman]] 是官方列名的贡献者及历史发布参与者；项目创始作者与当前维护者名单仍待验证。（raw 第 2–3 节）

## 与既有知识的关系

- 派生 [[google-uuid-go]] 与 [[paul-borman]]。`pborman/uuid` 和 `pborman/getopt` 只作为人物页中的未摄入项目线索。
- 未发现与现有 wiki 页的冲突。

## 由本来源派生 / 更新的页面

- [[google-uuid-go]]
- [[paul-borman]]
