---
title: "github.com/xo/terminfo"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/xo-terminfo-go-official-research-2026-11-01.md]
---

# github.com/xo/terminfo

## 用途与适用场景

以纯 Go 读取终端 terminfo 数据。（[[xo-terminfo-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/xo/terminfo`；项目中执行 `go get github.com/xo/terminfo`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```go
ti, err := terminfo.LoadFromEnv(); _, _ = ti, err
```

## 关键限制

- 依赖运行环境的 TERM 和 terminfo 数据；仓库是上游 fork。

## 来源

- [[xo-terminfo-go-official-research]]；[官方仓库](https://github.com/xo/terminfo)；[README 或版本文档](https://github.com/xo/terminfo)。
- 本地笔记：`raw/xo-terminfo-go-official-research-2026-11-01.md`。
