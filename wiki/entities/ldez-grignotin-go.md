---
title: "github.com/ldez/grignotin"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/ldez-grignotin-go-official-research-2026-11-01.md]
---

# github.com/ldez/grignotin

## 用途与适用场景

提供 Go proxy、模块元信息、版本及 `go env` 相关的辅助包；例如查询一个模块的可用版本。（[[ldez-grignotin-go-official-research]]）

## 依赖与版本

- 在 Go 项目中执行 `go get github.com/ldez/grignotin`；实际 import 使用所需子包，如 `github.com/ldez/grignotin/goproxy`。
- 2026-11-01 查阅官方 README；具体版本由项目锁定。收件箱的 `girgnotin` 与用户补充的 `ldex` 均已按官方路径消歧，原文未改。

## 作者与维护者

- 官方仓库关联账号：[[ldez-account]]；具体个人创建者与当前维护角色待验证。

## 典型用法

查询模块版本；需导入 `goproxy`、补齐外围函数，**未在本机运行**。

```go
client := goproxy.NewClient("")
versions, err := client.GetVersions("github.com/ldez/grignotin")
_, _ = versions, err
```

## 关键限制

- 查询依赖网络与 Go proxy；各子包 API 分开使用。

## 来源

- [[ldez-grignotin-go-official-research]]；[官方仓库](https://github.com/ldez/grignotin)。
- 本地笔记：`raw/ldez-grignotin-go-official-research-2026-11-01.md`。
