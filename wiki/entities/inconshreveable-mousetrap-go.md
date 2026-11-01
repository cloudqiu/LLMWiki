---
title: "github.com/inconshreveable/mousetrap"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/inconshreveable-mousetrap-go-official-research-2026-11-01.md]
---

# github.com/inconshreveable/mousetrap

## 用途与适用场景

检测 Windows 程序是否由 Explorer 双击启动。（[[inconshreveable-mousetrap-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/inconshreveable/mousetrap`；项目中执行 `go get github.com/inconshreveable/mousetrap`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```go
if mousetrap.StartedByExplorer() { /* show guidance */ }
```

## 关键限制

- 仅适用于 Windows 场景。

## 来源

- [[inconshreveable-mousetrap-go-official-research]]；[官方仓库](https://github.com/inconshreveable/mousetrap)；[所查 README 或仓库说明](https://raw.githubusercontent.com/inconshreveable/mousetrap/master/README.md)。
- 本地笔记：`raw/inconshreveable-mousetrap-go-official-research-2026-11-01.md`。
