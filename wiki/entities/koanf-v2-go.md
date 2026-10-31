---
title: "github.com/knadh/koanf/v2"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/koanf-v2-go-official-research-2026-10-31.md]
---

# github.com/knadh/koanf/v2

## 用途与适用场景

从多种 provider 与 parser 加载、合并和读取配置。（[[koanf-v2-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/knadh/koanf/v2`；示例使用 `github.com/knadh/koanf/v2`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- [[kailash-nadh]]：项目原始署名与发布参与；完整维护名单待验证。
- 其他相关项目：[goyesql](https://github.com/knadh/goyesql)、[stuffbin](https://github.com/knadh/stuffbin)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
k := koanf.New(".")
fmt.Println(k.String("app.name"))
```

## 关键限制

- New 只创建空配置；必须 Load 才能读到值。收件箱写作 knadn，官方账号是 knadh。

## 来源

- [[koanf-v2-go-official-research]]
- [官方仓库](https://github.com/knadh/koanf)；[Go Packages](https://pkg.go.dev/github.com/knadh/koanf/v2)；[示例 API](https://pkg.go.dev/github.com/knadh/koanf/v2)。
- 本地查阅记录：`raw/koanf-v2-go-official-research-2026-10-31.md`。
