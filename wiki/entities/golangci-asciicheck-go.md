---
title: "github.com/golangci/asciicheck"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/golangci-asciicheck-go-official-research-2026-11-01.md]
---

# github.com/golangci/asciicheck

## 用途与适用场景

检查 Go 标识符中的非 ASCII 字符。（[[golangci-asciicheck-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/golangci/asciicheck`；在项目中执行 `go get github.com/golangci/asciicheck`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 官方仓库归属账号：[[golangci]]；这只确认账号关联。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```sh
golangci-lint run --enable-only asciicheck ./...
```

## 关键限制

- CLI 参数需按 golangci-lint 目标版本复核。

## 来源

- [[golangci-asciicheck-go-official-research]]；[官方仓库](https://github.com/golangci/asciicheck)；[所查 README 或仓库说明](https://github.com/golangci/asciicheck)。
- 本地查阅记录：`raw/golangci-asciicheck-go-official-research-2026-11-01.md`。
