# dario.cat/mergo 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`dario.cat/mergo`。
- 官方模块：`dario.cat/mergo`。
- 用途：把源结构体或 map 的值合并到目标，常用于填入默认配置。
- [官方项目或文档](https://dario.cat/mergo/)；[Go Packages](https://pkg.go.dev/dario.cat/mergo)。

## 安装与典型用法

```go
go get dario.cat/mergo
```

```go
dst := struct{ Name string }{}
src := struct{ Name string }{Name: "default"}
if err := mergo.Merge(&dst, src); err != nil { panic(err) }
```

## 身份与边界

- 身份：Dario Castañé 在官方个人页明确称 Mergo 为其项目；具体共同维护者待验证。
- 限制：默认只填目标零值；WithOverride 会改变覆盖行为；目标参数需可写。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
