---
title: "chi v5 官方资料查阅记录"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, chi, http]
status: growing
sources: [raw/chi-official-research-2026-10-31.md]
author: "go-chi 项目、Go Packages；查阅记录由 Codex 整理"
source_url: "https://pkg.go.dev/github.com/go-chi/chi/v5"
raw_file: raw/chi-official-research-2026-10-31.md
format: notes
---

# chi v5 官方资料查阅记录

## 来源信息

- 来源：[Go Packages chi（查阅时显示 v5.5.0）](https://pkg.go.dev/github.com/go-chi/chi/v5)、[chi 官方仓库](https://github.com/go-chi/chi)、[Peter Kieltyka 主页](https://github.com/pkieltyka)、[webrpc 官方仓库](https://github.com/webrpc/webrpc)。
- 查阅日期：2026-10-31；本地文件：`raw/chi-official-research-2026-10-31.md`。直接下载官方原文失败，本地文件是带链接和章节定位的查阅笔记。

## 一句话概括

> chi v5 是兼容 Go 标准库 `net/http` 的轻量路由库，可用路由参数与 middleware 组织 HTTP 服务。

## 核心要点

- 模块路径 `github.com/go-chi/chi/v5`；本次查阅 v5.5.0 的 API，未核定用户本地版本。（raw 第 1 节）
- 核心路由可用 `NewRouter`、`Get` 与 `URLParam`；可组合标准 `net/http` handler 与 middleware。（raw 第 1 节）
- 官方资料确认 [[peter-kieltyka]] 是 chi 作者；webrpc 官方 README 另列其为共同作者。chi 当前维护者名单尚待验证。（raw 第 2–3 节）

## 与既有知识的关系

- 派生 [[chi-go]] 和 [[peter-kieltyka]]；其他库只作作者页的查询线索，尚未摄入。
- 未发现与现有 wiki 页的冲突。

## 由本来源派生 / 更新的页面

- [[chi-go]]
- [[peter-kieltyka]]

## 留给用户的讨论问题

- 下一项待摄入库应按收件箱顺序处理，或由用户指定优先级。
