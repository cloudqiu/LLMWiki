---
title: "github.com/sashamelentyev/interfacebloat"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/sashamelentyev-interfacebloat-go-official-research-2026-11-01.md]
---

# github.com/sashamelentyev/interfacebloat

## 用途与适用场景

检查接口方法数是否过多。（[[sashamelentyev-interfacebloat-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/sashamelentyev/interfacebloat`；项目中执行 `go get github.com/sashamelentyev/interfacebloat`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 官方账号关联：[[sashamelentyev-account]]；这不单独证明创建者或现任维护者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```sh
interfacebloat ./...
```

## 关键限制

- 接口长度阈值是设计约定，不直接说明缺陷。

## 来源

- [[sashamelentyev-interfacebloat-go-official-research]]；[官方仓库](https://github.com/sashamelentyev/interfacebloat)；[README 或版本文档](https://raw.githubusercontent.com/sashamelentyev/interfacebloat/master/README.md)。
- 本地笔记：`raw/sashamelentyev-interfacebloat-go-official-research-2026-11-01.md`。
