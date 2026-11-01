---
title: "github.com/manuelarte/funcorder"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/manuelarte-funcorder-go-official-research-2026-11-01.md]
---

# github.com/manuelarte/funcorder

## 用途与适用场景

检查 Go 类型方法和构造函数的顺序。（[[manuelarte-funcorder-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/manuelarte/funcorder`；项目中执行 `go get github.com/manuelarte/funcorder`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 官方仓库关联账号：[[manuelarte-account]]；具体创建和维护角色待核实。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```sh
golangci-lint run --enable-only funcorder ./...
```

## 关键限制

- 排序规则是代码风格约定。

## 来源

- [[manuelarte-funcorder-go-official-research]]；[官方仓库](https://github.com/manuelarte/funcorder)；[所查 README 或仓库说明](https://github.com/manuelarte/funcorder)。
- 本地笔记：`raw/manuelarte-funcorder-go-official-research-2026-11-01.md`。
