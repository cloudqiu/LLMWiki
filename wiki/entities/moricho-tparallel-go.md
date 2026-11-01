---
title: "github.com/moricho/tparallel"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/moricho-tparallel-go-official-research-2026-11-01.md]
---

# github.com/moricho/tparallel

## 用途与适用场景

检查不恰当的 t.Parallel 使用。（[[moricho-tparallel-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/moricho/tparallel`；项目中执行 `go get github.com/moricho/tparallel`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```sh
golangci-lint run --enable-only tparallel ./...
```

## 关键限制

- 并行测试约束按共享状态和测试框架核对。

## 来源

- [[moricho-tparallel-go-official-research]]；[官方仓库](https://github.com/moricho/tparallel)；[所查 README 或仓库说明](https://github.com/moricho/tparallel)。
- 本地笔记：`raw/moricho-tparallel-go-official-research-2026-11-01.md`。
