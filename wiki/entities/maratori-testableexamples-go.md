---
title: "github.com/maratori/testableexamples"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/maratori-testableexamples-go-official-research-2026-11-01.md]
---

# github.com/maratori/testableexamples

## 用途与适用场景

检查 Go Example 是否声明可验证输出。（[[maratori-testableexamples-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/maratori/testableexamples`；项目中执行 `go get github.com/maratori/testableexamples`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。收件箱原条目为 `github.com/maratori/testableexemples`。

## 作者与维护者

- 官方仓库关联账号：[[maratori-account]]；具体创建和维护角色待核实。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```sh
golangci-lint run --enable-only testableexamples ./...
```

## 关键限制

- 只保证示例可被测试框架验证，不保证示例质量。

## 来源

- [[maratori-testableexamples-go-official-research]]；[官方仓库](https://github.com/maratori/testableexamples)；[所查 README 或仓库说明](https://github.com/maratori/testableexamples)。
- 本地笔记：`raw/maratori-testableexamples-go-official-research-2026-11-01.md`。
