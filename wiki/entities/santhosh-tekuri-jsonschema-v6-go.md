---
title: "github.com/santhosh-tekuri/jsonschema/v6"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/santhosh-tekuri-jsonschema-v6-go-official-research-2026-11-01.md]
---

# github.com/santhosh-tekuri/jsonschema/v6

## 用途与适用场景

编译和验证 JSON Schema。（[[santhosh-tekuri-jsonschema-v6-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/santhosh-tekuri/jsonschema/v6`；项目中执行 `go get github.com/santhosh-tekuri/jsonschema/v6`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```go
compiler := jsonschema.NewCompiler(); schema, err := compiler.Compile("schema.json"); _, _ = schema, err
```

## 关键限制

- v6 与 v5 API 需区分；示例文件路径需按实际 loader 设置。

## 来源

- [[santhosh-tekuri-jsonschema-v6-go-official-research]]；[官方仓库](https://github.com/santhosh-tekuri/jsonschema)；[README 或版本文档](https://pkg.go.dev/github.com/santhosh-tekuri/jsonschema/v6)。
- 本地笔记：`raw/santhosh-tekuri-jsonschema-v6-go-official-research-2026-11-01.md`。
