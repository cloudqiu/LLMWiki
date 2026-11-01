---
title: "github.com/mattn/go-runewidth"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/mattn-go-runewidth-go-official-research-2026-11-01.md]
---

# github.com/mattn/go-runewidth

## 用途与适用场景

计算终端中的 Unicode 字符显示宽度。（[[mattn-go-runewidth-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/mattn/go-runewidth`；项目中执行 `go get github.com/mattn/go-runewidth`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```go
width := runewidth.StringWidth("世界"); _ = width
```

## 关键限制

- 终端实际宽度可能与 Unicode 宽度表不同。

## 来源

- [[mattn-go-runewidth-go-official-research]]；[官方仓库](https://github.com/mattn/go-runewidth)；[所查 README 或仓库说明](https://raw.githubusercontent.com/mattn/go-runewidth/master/README.md)。
- 本地笔记：`raw/mattn-go-runewidth-go-official-research-2026-11-01.md`。
