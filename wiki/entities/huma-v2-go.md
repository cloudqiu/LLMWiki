---
title: "github.com/danielgtaylor/huma/v2"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/huma-v2-go-official-research-2026-10-31.md]
---

# github.com/danielgtaylor/huma/v2

## 用途与适用场景

以 Go 类型定义 HTTP API 并生成 OpenAPI 文档与验证逻辑。（[[huma-v2-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/danielgtaylor/huma/v2`；示例同时使用 `github.com/danielgtaylor/huma/v2` 与 `github.com/danielgtaylor/huma/v2/adapters/humago`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 作者索引：[[daniel-g-taylor]]。
- 项目账号 danielgtaylor；近期发布由其他贡献者参与，不能视为唯一维护者。
- 其他相关项目：[restish](https://github.com/danielgtaylor/restish)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
r := http.NewServeMux()
api := humago.New(r, huma.DefaultConfig("Demo", "1.0"))
huma.Get(api, "/hello", func(ctx context.Context, in *struct{}) (*struct{ Body string }, error) {
    return &struct{ Body string }{Body: "hello"}, nil
})
```

## 关键限制

- 需要适配器子包；此片段使用 humago。HTTP 服务启动及请求验证仍需按实际 router 配置。

## 来源

- [[huma-v2-go-official-research]]
- [官方仓库](https://github.com/danielgtaylor/huma)；[Go Packages](https://pkg.go.dev/github.com/danielgtaylor/huma/v2)；[humago 适配器](https://pkg.go.dev/github.com/danielgtaylor/huma/v2/adapters/humago)。
- 本地查阅记录：`raw/huma-v2-go-official-research-2026-10-31.md`。
