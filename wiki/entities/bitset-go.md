---
title: "github.com/bits-and-blooms/bitset"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/bitset-go-official-research-2026-11-01.md]
---

# github.com/bits-and-blooms/bitset

## 用途与适用场景

用可扩展位集合存储非负整数的布尔状态。（[[bitset-go-official-research]]）

## 依赖与版本

- 模块：`github.com/bits-and-blooms/bitset`；安装或依赖声明：`go get github.com/bits-and-blooms/bitset`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- 仓库账号 bits-and-blooms；个人创建者和当前维护者待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```go
b := bitset.New(128).Set(10); ok := b.Test(10); _ = ok
```

## 关键限制

- 容量随最大设置位增长，清除位不会自动缩小内存。

## 来源

- [[bitset-go-official-research]]；[官方资料](https://pkg.go.dev/github.com/bits-and-blooms/bitset)；[Go Packages](https://pkg.go.dev/github.com/bits-and-blooms/bitset)。
- 本地研究笔记：`raw/bitset-go-official-research-2026-11-01.md`。
