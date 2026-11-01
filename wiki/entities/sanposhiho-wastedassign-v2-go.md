---
title: "github.com/sanposhiho/wastedassign/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/sanposhiho-wastedassign-v2-go-official-research-2026-11-01.md]
---

# github.com/sanposhiho/wastedassign/v2

## 用途与适用场景

检测赋值后未使用就被覆盖的值。（[[sanposhiho-wastedassign-v2-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/sanposhiho/wastedassign/v2`；项目中执行 `go get github.com/sanposhiho/wastedassign/v2`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```sh
go vet -vettool=$(which wastedassign) ./...
```

## 关键限制

- 示例来自官方 README；Windows 需替换 shell 命令替换语法。

## 来源

- [[sanposhiho-wastedassign-v2-go-official-research]]；[官方仓库](https://github.com/sanposhiho/wastedassign)；[README 或版本文档](https://raw.githubusercontent.com/sanposhiho/wastedassign/master/README.md)。
- 本地笔记：`raw/sanposhiho-wastedassign-v2-go-official-research-2026-11-01.md`。
