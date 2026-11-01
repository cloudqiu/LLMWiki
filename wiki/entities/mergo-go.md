---
title: "dario.cat/mergo"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/mergo-go-official-research-2026-11-01.md]
---

# dario.cat/mergo

## 用途与适用场景

把源结构体或 map 的值合并到目标，常用于填入默认配置。（[[mergo-go-official-research]]）

## 依赖与版本

- 官方模块：`dario.cat/mergo`。
- 安装或依赖声明：`go get dario.cat/mergo`。
- 查阅日期：2026-11-01；具体版本以目标项目锁定为准。

## 作者与维护者

- [[dario-castane]]；Dario Castañé 在官方个人页明确称 Mergo 为其项目；具体共同维护者待验证。

## 典型用法

下面示例以官方文档或项目 README 为依据；**未在本机运行**。命令需在适当 Go 项目中执行；Go 代码片段需补齐 import 与外围函数。

```go
dst := struct{ Name string }{}
src := struct{ Name string }{Name: "default"}
if err := mergo.Merge(&dst, src); err != nil { panic(err) }
```

## 关键限制

- 默认只填目标零值；WithOverride 会改变覆盖行为；目标参数需可写。

## 来源

- [[mergo-go-official-research]]；[官方项目或文档](https://dario.cat/mergo/)；[Go Packages](https://pkg.go.dev/dario.cat/mergo)。
- 本地原始资料：`raw/mergo-go-official-research-2026-11-01.md`。
