---
title: "github.com/sivchari/containedctx"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/sivchari-containedctx-go-official-research-2026-11-01.md]
---

# github.com/sivchari/containedctx

## 用途与适用场景

检查 struct 字段中保存 context.Context 的做法。（[[sivchari-containedctx-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/sivchari/containedctx`；项目中执行 `go get github.com/sivchari/containedctx`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```sh
golangci-lint run --enable-only containedctx ./...
```

## 关键限制

- 是否保留 context 需结合对象生命周期判断。

## 来源

- [[sivchari-containedctx-go-official-research]]；[官方仓库](https://github.com/sivchari/containedctx)；[README 或版本文档](https://github.com/sivchari/containedctx)。
- 本地笔记：`raw/sivchari-containedctx-go-official-research-2026-11-01.md`。
