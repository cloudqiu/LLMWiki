---
title: "github.com/knadh/koanf/providers/rawbytes"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/koanf-rawbytes-go-official-research-2026-10-31.md]
---

# github.com/knadh/koanf/providers/rawbytes

## 用途与适用场景

把内存中的 []byte 作为 koanf 配置源；常与 JSON、TOML 等 parser 配合。（[[koanf-rawbytes-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/knadh/koanf/providers/rawbytes`；示例使用 `github.com/knadh/koanf/providers/rawbytes`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- [[kailash-nadh]]：koanf 项目原始署名；子模块的独立作者待验证。
- 其他相关项目：[goyesql](https://github.com/knadh/goyesql)、[stuffbin](https://github.com/knadh/stuffbin)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
k := koanf.New(".")
err := k.Load(rawbytes.Provider([]byte(`{"port":8080}`)), json.Parser())
fmt.Println(k.Int("port"), err)
```

## 关键限制

- 只提供原始字节，不负责解析格式；需要另配 parser。收件箱写作 rawybytes，官方路径为 rawbytes。

## 来源

- [[koanf-rawbytes-go-official-research]]
- [官方仓库](https://github.com/knadh/koanf)；[Go Packages](https://pkg.go.dev/github.com/knadh/koanf/providers/rawbytes)；[示例 API](https://pkg.go.dev/github.com/knadh/koanf/providers/rawbytes)。
- 本地查阅记录：`raw/koanf-rawbytes-go-official-research-2026-10-31.md`。
