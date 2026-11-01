---
title: "github.com/jjti/go-spancheck"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/jjti-go-spancheck-go-official-research-2026-11-01.md]
---

# github.com/jjti/go-spancheck

## 用途与适用场景

检查追踪 span 是否正确结束及设置状态。（[[jjti-go-spancheck-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/jjti/go-spancheck`；项目中执行 `go get github.com/jjti/go-spancheck`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```sh
spancheck -checks 'end,set-status,record-error' ./...
```

## 关键限制

- 对 OpenTelemetry 与 OpenCensus 的支持按目标版本核对。

## 来源

- [[jjti-go-spancheck-go-official-research]]；[官方仓库](https://github.com/jjti/go-spancheck)；[所查 README 或仓库说明](https://raw.githubusercontent.com/jjti/go-spancheck/main/README.md)。
- 本地笔记：`raw/jjti-go-spancheck-go-official-research-2026-11-01.md`。
