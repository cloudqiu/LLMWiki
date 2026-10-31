---
title: "koanf TOML parser v2 (Go)"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, koanf, toml, config]
status: growing
sources: [raw/koanf-toml-v2-official-research-2026-10-31.md]
---

# koanf TOML parser v2

## 用途与适用场景

为 koanf 配置管理库提供 TOML 字节的解析与序列化。适合已有 koanf 核心、需要从文件或其他来源加载 TOML 配置的程序；它负责**格式解析**，实际读取文件、环境变量等由 provider 负责。（[[koanf-toml-v2-official-research]]；raw 第 1 节）

## 依赖与版本

- 语言 / 生态：Go；parser 模块路径 `github.com/knadh/koanf/parsers/toml/v2`。
- 查阅版本 / 日期：Go Packages 显示 parser v2.2.2；2026-10-31。用户项目版本待验证。
- 与 koanf 联用时分别安装核心 `github.com/knadh/koanf/v2`、此 parser，以及所需 provider；本例用 `github.com/knadh/koanf/providers/file`。parser 源码依赖 `github.com/pelletier/go-toml/v2`。（raw 第 1 节）

## 作者与维护者

- koanf 项目原始版权署名：[[kailash-nadh]]；该项目 LICENSE 有其姓名，`knadh` 近期发布 koanf 版本。（raw 第 2 节）
- 此 parser 子模块的独立作者与完整当前维护者名单：**待验证**；不将仓库归属等同于个人独立创作。（raw 第 3 节）

## 典型用法

在 Go 模块中安装 `github.com/knadh/koanf/v2`、`github.com/knadh/koanf/parsers/toml/v2` 和 `github.com/knadh/koanf/providers/file`。保存以下两个文件后执行 `go run .`。示例根据官方 README 的 `Load` 模式和 parser API 组成，**尚未实际运行**。（raw 第 1 节）

`config.toml`：

```toml
[app]
name = "demo"
```

`main.go`：

```go
package main

import (
    "fmt"
    "log"

    "github.com/knadh/koanf/v2"
    "github.com/knadh/koanf/parsers/toml/v2"
    "github.com/knadh/koanf/providers/file"
)

func main() {
    k := koanf.New(".")
    if err := k.Load(file.Provider("config.toml"), toml.Parser()); err != nil {
        log.Fatal(err)
    }
    fmt.Println(k.String("app.name")) // demo
}
```

## 关键限制

- parser 不独立提供配置来源；从文件读取必须另装并调用 provider，同时需要 koanf 核心实例。（raw 第 1 节）
- `parsers/toml` 与 `parsers/toml/v2` 是不同模块路径；本页针对后者，其底层是 `go-toml/v2`。（raw 第 1 节）
- v2.2.2 源码在空 map 解析或序列化时返回 `(nil, nil)`；依赖空输入行为的程序应按实际版本核对。（raw 第 1 节）

## 来源

- [[koanf-toml-v2-official-research]]
- [官方仓库与 README](https://github.com/knadh/koanf)
- [Go Packages 文档](https://pkg.go.dev/github.com/knadh/koanf/parsers/toml/v2)
- [v2.2.2 源码](https://github.com/knadh/koanf/blob/parsers/toml/v2.2.2/parsers/toml/toml.go)
- 本地查阅记录：`raw/koanf-toml-v2-official-research-2026-10-31.md`
