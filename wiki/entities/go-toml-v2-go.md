---
title: "github.com/pelletier/go-toml/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/go-toml-v2-go-official-research-2026-11-01.md]
---

# github.com/pelletier/go-toml/v2

## 用途与适用场景

把 TOML 文本解码为 Go 结构，也可将结构编码为 TOML。（[[go-toml-v2-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/pelletier/go-toml/v2`；示例使用 `github.com/pelletier/go-toml/v2`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[thomas-pelletier]]：Thomas Pelletier 的官方 GitHub 主页将 go-toml 列为项目；具体版本维护者名单待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
var cfg struct { Name string `toml:"name"` }
err := toml.Unmarshal([]byte("name = \"demo\""), &cfg)
if err != nil { panic(err) }
fmt.Println(cfg.Name)
```

## 关键限制

- 收件箱 pelleiter 为拼写错误；官方模块路径为 pelletier。TOML v2 与 v1 是不同导入路径。

## 来源

- [[go-toml-v2-go-official-research]]；本地查阅记录：`raw/go-toml-v2-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/pelletier/go-toml)；[Go Packages](https://pkg.go.dev/github.com/pelletier/go-toml/v2)。
