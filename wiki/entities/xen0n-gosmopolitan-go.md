---
title: "github.com/xen0n/gosmopolitan"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/xen0n-gosmopolitan-go-official-research-2026-11-01.md]
---

# github.com/xen0n/gosmopolitan

## 用途与适用场景

检查可能妨碍国际化和本地化的 Go 代码模式。（[[xen0n-gosmopolitan-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/xen0n/gosmopolitan`；项目中执行 `go get github.com/xen0n/gosmopolitan`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```sh
golangci-lint run --enable-only gosmopolitan ./...
```

## 关键限制

- 规则特别针对非拉丁文字和本地时区用法，不适合所有项目。

## 来源

- [[xen0n-gosmopolitan-go-official-research]]；[官方仓库](https://github.com/xen0n/gosmopolitan)；[README 或版本文档](https://github.com/xen0n/gosmopolitan)。
- 本地笔记：`raw/xen0n-gosmopolitan-go-official-research-2026-11-01.md`。
