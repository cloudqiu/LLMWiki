---
title: "github.com/kulti/thelper"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/kulti-thelper-go-official-research-2026-11-01.md]
---

# github.com/kulti/thelper

## 用途与适用场景

检查测试辅助函数是否调用 t.Helper。（[[kulti-thelper-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/kulti/thelper`；项目中执行 `go get github.com/kulti/thelper`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```sh
golangci-lint run --enable-only thelper ./...
```

## 关键限制

- 适用于 testing.T、B 等测试助手。

## 来源

- [[kulti-thelper-go-official-research]]；[官方仓库](https://github.com/kulti/thelper)；[所查 README 或仓库说明](https://raw.githubusercontent.com/kulti/thelper/master/README.md)。
- 本地笔记：`raw/kulti-thelper-go-official-research-2026-11-01.md`。
