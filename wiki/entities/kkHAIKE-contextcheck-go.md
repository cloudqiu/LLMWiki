---
title: "github.com/kkHAIKE/contextcheck"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/kkHAIKE-contextcheck-go-official-research-2026-11-01.md]
---

# github.com/kkHAIKE/contextcheck

## 用途与适用场景

检查 context 是否沿调用链继承和传递。（[[kkHAIKE-contextcheck-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/kkHAIKE/contextcheck`；项目中执行 `go get github.com/kkHAIKE/contextcheck`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```sh
golangci-lint run --enable-only contextcheck ./...
```

## 关键限制

- 跨函数传播分析可能受代码结构和配置影响。

## 来源

- [[kkHAIKE-contextcheck-go-official-research]]；[官方仓库](https://github.com/kkHAIKE/contextcheck)；[所查 README 或仓库说明](https://raw.githubusercontent.com/kkHAIKE/contextcheck/master/README.md)。
- 本地笔记：`raw/kkHAIKE-contextcheck-go-official-research-2026-11-01.md`。
