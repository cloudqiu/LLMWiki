---
title: "github.com/dave/dst"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/dave-dst-go-official-research-2026-11-01.md]
---

# github.com/dave/dst

## 用途与适用场景

保留注释和间距地改写 Go 语法树。（[[dave-dst-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/dave/dst`；在项目中执行 `go get github.com/dave/dst`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 作者待验证；仓库归属账号不等于已核实的个人创建者。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
f, err := decorator.Parse(`package p
var X = 1`); _ = f; _ = err
```

## 关键限制

- 示例须导入 github.com/dave/dst/decorator。

## 来源

- [[dave-dst-go-official-research]]；[官方仓库](https://github.com/dave/dst)；[所查 README 或仓库说明](https://raw.githubusercontent.com/dave/dst/master/README.md)。
- 本地查阅记录：`raw/dave-dst-go-official-research-2026-11-01.md`。
