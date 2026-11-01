---
title: "github.com/golangci/revgrep"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/golangci-revgrep-go-official-research-2026-11-01.md]
---

# github.com/golangci/revgrep

## 用途与适用场景

只显示变更行上的静态分析结果。（[[golangci-revgrep-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/golangci/revgrep`；在项目中执行 `go get github.com/golangci/revgrep`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 官方仓库归属账号：[[golangci]]；这只确认账号关联。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```sh
go vet ./... 2>&1 | revgrep HEAD~1
```

## 关键限制

- 依赖 Git 差异和输入诊断格式。

## 来源

- [[golangci-revgrep-go-official-research]]；[官方仓库](https://github.com/golangci/revgrep)；[所查 README 或仓库说明](https://github.com/golangci/revgrep)。
- 本地查阅记录：`raw/golangci-revgrep-go-official-research-2026-11-01.md`。
