---
title: "gophernotes 官方资料查阅记录"
type: source
created: 2026-10-31
updated: 2026-10-31
tags: [go, jupyter, gophernotes]
status: growing
sources: [raw/gophernotes-official-research-2026-10-31.md, raw/gophernotes-usage.md]
author: "gopherdata；查阅记录由 Codex 整理"
source_url: "https://github.com/gopherdata/gophernotes"
raw_file: raw/gophernotes-official-research-2026-10-31.md
format: notes
---

# gophernotes 官方资料查阅记录

## 来源信息

- 官方项目：[gopherdata/gophernotes](https://github.com/gopherdata/gophernotes)
- 官方原文：[README](https://github.com/gopherdata/gophernotes/blob/master/README.md)、[complete.go](https://github.com/gopherdata/gophernotes/blob/master/complete.go)
- 本地查阅记录：`raw/gophernotes-official-research-2026-10-31.md`；先前使用笔记：`raw/gophernotes-usage.md`
- 查阅日期：2026-10-31；直接下载官方原文失败，因此本地文件并非官方原文快照。

## 一句话概括

> gophernotes 让 Go 代码在 Jupyter 中按单元交互执行，适合教学、探索与可分享的示范笔记。

## 核心要点

- 使用 `gomacro` 解释执行；在 Jupyter 选择 Go kernel 后直接运行代码单元。（查阅记录「官方项目 README」）
- 支持 `%help` 等专用命令；补全由 kernel 的 completion handler 提供，但自动弹窗行为取决于前端。（查阅记录「官方项目 README」「官方补全实现」）
- 原生 Windows 下导入第三方 Go 包受 `plugin` 限制；README 建议需要这类包时使用 Docker。（查阅记录「官方项目 README」）

## 与既有知识的关系

- 衍生库页：[[gophernotes-go]]。
- 用户已报告本地启动 gophernotes，但实际版本、前端、执行和补全情况均待验证。

## 由本来源派生 / 更新的页面

- [[gophernotes-go]]
