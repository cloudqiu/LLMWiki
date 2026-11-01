---
title: "github.com/tommy-muehle/go-mnd/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/tommy-muehle-go-mnd-v2-go-official-research-2026-11-01.md]
---

# github.com/tommy-muehle/go-mnd/v2

## 用途与适用场景

检测 Go 代码中的魔法数字。（[[tommy-muehle-go-mnd-v2-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/tommy-muehle/go-mnd/v2`；项目中执行 `go get github.com/tommy-muehle/go-mnd/v2`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```sh
golangci-lint run --enable-only mnd ./...
```

## 关键限制

- 数字常量的可接受性依赖上下文和规则配置。

## 来源

- [[tommy-muehle-go-mnd-v2-go-official-research]]；[官方仓库](https://github.com/tommy-muehle/go-mnd)；[README 或版本文档](https://github.com/tommy-muehle/go-mnd)。
- 本地笔记：`raw/tommy-muehle-go-mnd-v2-go-official-research-2026-11-01.md`。
