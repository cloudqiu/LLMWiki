---
title: "github.com/stretchr/testify"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/stretchr-testify-go-official-research-2026-11-01.md]
---

# github.com/stretchr/testify

## 用途与适用场景

提供 Go 测试断言、mock 与 suite。（[[stretchr-testify-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/stretchr/testify`；项目中执行 `go get github.com/stretchr/testify`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 官方账号关联：[[stretchr-account]]；这不单独证明创建者或现任维护者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```go
assert.Equal(t, want, got)
```

## 关键限制

- 官方说明 v1 继续维护且不接受破坏性变更；示例需位于测试函数。

## 来源

- [[stretchr-testify-go-official-research]]；[官方仓库](https://github.com/stretchr/testify)；[README 或版本文档](https://raw.githubusercontent.com/stretchr/testify/master/README.md)。
- 本地笔记：`raw/stretchr-testify-go-official-research-2026-11-01.md`。
