---
title: "github.com/mitchellh/reflectwalk"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/reflectwalk-go-official-research-2026-11-01.md]
---

# github.com/mitchellh/reflectwalk

## 用途与适用场景

按反射方式遍历复杂 Go 值，并通过 walker 接口处理节点。（[[reflectwalk-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/mitchellh/reflectwalk`；示例使用 `github.com/mitchellh/reflectwalk`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[mitchell-hashimoto]]：mitchellh 账号仓库；个人独立创建者未从仓库归属证实；仓库已归档。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
err := reflectwalk.Walk(value, walker) // walker 实现所需接口
```

## 关键限制

- walker 必须实现 PrimitiveWalker、StructWalker 等所需回调；原仓库已归档为只读。

## 来源

- [[reflectwalk-go-official-research]]；本地查阅记录：`raw/reflectwalk-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/mitchellh/reflectwalk)；[Go Packages](https://pkg.go.dev/github.com/mitchellh/reflectwalk)。
