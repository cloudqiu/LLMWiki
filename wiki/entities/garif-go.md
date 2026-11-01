---
title: "codeberg.org/chavacava/garif"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/garif-go-official-research-2026-11-01.md]
---

# codeberg.org/chavacava/garif

## 用途与适用场景

构造、修改并输出 SARIF 2.1.0 静态分析结果日志。（[[garif-go-official-research]]）

## 依赖与版本

- 官方模块：`codeberg.org/chavacava/garif`。
- 安装或依赖声明：`go get codeberg.org/chavacava/garif`。
- 查阅日期：2026-11-01；具体版本以目标项目锁定为准。

## 作者与维护者

- Codeberg 账号 chavacava；个人身份与当前维护者待验证。

## 典型用法

下面示例以官方文档或项目 README 为依据；**未在本机运行**。命令需在适当 Go 项目中执行；Go 代码片段需补齐 import 与外围函数。

```go
rule := garif.NewRule("example")
driver := garif.NewDriver("my-analyzer").WithRules(rule)
_ = driver
```

## 关键限制

- Go Packages 的 README 示例仍写旧 GitHub import；实际依赖应使用 Codeberg 模块路径，具体迁移兼容性待验证。

## 来源

- [[garif-go-official-research]]；[官方项目或文档](https://pkg.go.dev/codeberg.org/chavacava/garif)；[Go Packages](https://pkg.go.dev/codeberg.org/chavacava/garif)。
- 本地原始资料：`raw/garif-go-official-research-2026-11-01.md`。
