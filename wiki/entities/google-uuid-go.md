---
title: "google/uuid (Go)"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, uuid]
status: growing
sources: [raw/google-uuid-official-research-2026-10-31.md]
---

# google/uuid

## 用途与适用场景

用于在 Go 程序中生成、解析和检查 UUID。适合为记录或请求生成 UUID，以及解析外部输入的 UUID 字符串；`UUID` 是可直接比较、可作 map key 的 16 字节数组。（[[google-uuid-official-research]]；raw 第 1 节）

## 依赖与版本

- 语言 / 生态：Go；模块路径 `github.com/google/uuid`。
- 查阅版本 / 日期：Go Packages 显示 v1.6.0；2026-10-31。用户项目版本待验证。
- 在 Go 模块项目中执行 `go get github.com/google/uuid`。（raw 第 1 节「Install」）

## 作者与维护者

- 创始作者：**待验证**。仓库位于 Google 组织，源码版权行署名 Google Inc.，但这些信息不等同于具体作者名单。（raw 第 2–3 节）
- 已确认贡献者与历史发布参与者：[[paul-borman]]；官方 `CONTRIBUTORS` 列名 Paul Borman，历史 release 由 `pborman` 账号发布。此处不把他写成唯一作者或当前维护者。（raw 第 2 节）
- 当前维护者：**待验证**。（raw 第 3 节）

## 典型用法

在已运行 `go mod init` 和上述 `go get` 的目录中保存为 `main.go`，执行 `go run .`。此例依据官方 `NewRandom`、`String`、`Parse` API 编写，**尚未实际运行**。（raw 第 1 节）

```go
package main

import (
    "fmt"
    "log"

    "github.com/google/uuid"
)

func main() {
    id, err := uuid.NewRandom()
    if err != nil {
        log.Fatal(err)
    }

    parsed, err := uuid.Parse(id.String())
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println(parsed)
}
```

## 关键限制

- `Parse` 接受部分非标准字符串形式；若输入必须是某一种固定格式，须额外检查格式。（raw 第 1 节「Parse」「Validate」）
- `NewString` 返回值方便，但随机数源失败时会 panic；需要处理错误时使用 `NewRandom`。（raw 第 1 节）
- 可选随机池在 Go heap 中保存随机数据；安全敏感场景需评估，且启用或关闭随机池时不能与 UUID 生成并发。（raw 第 1 节「EnableRandPool」）
- `google/uuid` 与其上游 `pborman/uuid` 的 `UUID` 类型不同，不能假设可直接替换。（raw 第 1–2 节）

## 来源

- [[google-uuid-official-research]]
- [官方仓库](https://github.com/google/uuid)
- [Go Packages 文档](https://pkg.go.dev/github.com/google/uuid)
- 本地查阅记录：`raw/google-uuid-official-research-2026-10-31.md`
