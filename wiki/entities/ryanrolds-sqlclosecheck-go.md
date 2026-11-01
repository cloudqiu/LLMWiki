---
title: "github.com/ryanrolds/sqlclosecheck"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/ryanrolds-sqlclosecheck-go-official-research-2026-11-01.md]
---

# github.com/ryanrolds/sqlclosecheck

## 用途与适用场景

检查 SQL Rows 与 Stmt 是否关闭。（[[ryanrolds-sqlclosecheck-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/ryanrolds/sqlclosecheck`；项目中执行 `go get github.com/ryanrolds/sqlclosecheck`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```sh
golangci-lint run --enable-only sqlclosecheck ./...
```

## 关键限制

- 分析器不能证明所有连接生命周期都正确。

## 来源

- [[ryanrolds-sqlclosecheck-go-official-research]]；[官方仓库](https://github.com/ryanrolds/sqlclosecheck)；[README 或版本文档](https://raw.githubusercontent.com/ryanrolds/sqlclosecheck/master/README.md)。
- 本地笔记：`raw/ryanrolds-sqlclosecheck-go-official-research-2026-11-01.md`。
