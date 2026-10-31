---
title: "github.com/samber/do"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/do-go-official-research-2026-10-31.md]
---

# github.com/samber/do

## 用途与适用场景

使用泛型注册、解析服务及管理依赖注入生命周期。（[[do-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/samber/do`；示例使用 `github.com/samber/do`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 作者索引：[[samuel-berthe]]。
- [[samuel-berthe]]：GitHub 自述将 do 列为其 Go 库。
- 其他相关项目：[lo](https://github.com/samber/lo)、[mo](https://github.com/samber/mo)、[oops](https://github.com/samber/oops)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
injector := do.New()
do.Provide(injector, func(*do.Injector) (int, error) { return 42, nil })
n, err := do.Invoke[int](injector)
fmt.Println(n, err)
```

## 关键限制

- 这是 v1 模块；v2 使用 github.com/samber/do/v2，迁移时核对 API。

## 来源

- [[do-go-official-research]]
- [官方仓库](https://github.com/samber/do)；[Go Packages](https://pkg.go.dev/github.com/samber/do)；[示例 API](https://pkg.go.dev/github.com/samber/do)。
- 本地查阅记录：`raw/do-go-official-research-2026-10-31.md`。
