---
title: "go.yaml.in/yaml/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/yaml-v2-go-official-research-2026-11-01.md]
---

# go.yaml.in/yaml/v2

## 用途与适用场景

将 YAML 编解码为 Go 值，提供严格解码以发现未知字段和重复键。（[[yaml-v2-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get go.yaml.in/yaml/v2`；示例使用 `go.yaml.in/yaml/v2`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[gustavo-niemeyer]]：官方 README 由 Gustavo Niemeyer 自述为早期项目并声明停止维护。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
var cfg struct { Name string `yaml:"name"` }
err := yaml.UnmarshalStrict([]byte("name: demo\n"), &cfg)
if err != nil { panic(err) }
```

## 关键限制

- 官方项目明确标为 unmaintained，仓库已归档；当前路径是 go.yaml.in/yaml/v2，旧 gopkg.in 路径须另行核对。

## 来源

- [[yaml-v2-go-official-research]]；本地查阅记录：`raw/yaml-v2-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/go-yaml/yaml)；[Go Packages](https://pkg.go.dev/go.yaml.in/yaml/v2)。
