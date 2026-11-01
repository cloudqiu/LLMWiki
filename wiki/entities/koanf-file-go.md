---
title: "github.com/knadh/koanf/providers/file"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library, koanf]
status: growing
sources: [raw/koanf-file-go-official-research-2026-11-01.md]
---

# github.com/knadh/koanf/providers/file

## 用途与适用场景

从磁盘读取 JSON、TOML 等配置文件的原始字节，配合对应 parser 加载到 [[koanf-v2-go]]；支持文件变更监听。（[[koanf-file-go-official-research]]）

## 依赖与版本

- Go 模块：`go get github.com/knadh/koanf/providers/file`；还须按配置格式安装 koanf 核心及 parser。
- 查阅日期：2026-11-01。Go Packages 检索页显示 v1.2.1；当前分支的 go.mod 声明 Go 1.23.0 和 fsnotify v1.9.0，不能据此推定 v1.2.1 的精确依赖。以目标项目 `go.mod` 为准。

## 作者与维护者

- [[kailash-nadh]]：koanf 项目 LICENSE 原始版权署名者，且参与近期版本发布。
- file 子模块的具体创建者和完整当前维护者名单待验证；仓库归属不等于唯一作者身份。

## 典型用法

先在项目中安装 `github.com/knadh/koanf/v2`、`github.com/knadh/koanf/providers/file`、`github.com/knadh/koanf/parsers/json`，并在运行目录创建 `config.json`，内容为 `{"app":{"name":"demo"}}`。以下示例依据官方 README 的 API 缩写，**未实际运行**。

```go
package main

import (
    "fmt"
    "log"

    "github.com/knadh/koanf/v2"
    "github.com/knadh/koanf/parsers/json"
    "github.com/knadh/koanf/providers/file"
)

func main() {
    k := koanf.New(".")
    if err := k.Load(file.Provider("config.json"), json.Parser()); err != nil {
        log.Fatal(err)
    }
    fmt.Println(k.String("app.name")) // demo
}
```

需要自动重载时，对同一个 `file.Provider(...)` 对象调用 `Watch(callback)`，在回调中处理错误并重新 `Load`，退出时调用 `Unwatch()`；并发读取配置时需自行加锁。（官方 README「Watching file for changes」）

## 关键限制

- provider 只提供字节，不能独自解析配置；`Read()` 不支持，必须配合 parser。
- README 对监听回调 `event` 的说明与当前源码存在差异；不要依赖未经目标版本核对的事件值。
- 文件不存在或读取失败会返回错误；监听与并发读取需考虑生命周期和同步。

## 来源

- [[koanf-file-go-official-research]]；本地研究笔记：`raw/koanf-file-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/knadh/koanf)、[包文档](https://pkg.go.dev/github.com/knadh/koanf/providers/file)、[官方 README](https://github.com/knadh/koanf/blob/master/README.md)。
