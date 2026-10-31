---
title: "go.uber.org/zap"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/zap-go-official-research-2026-10-31.md]
---

# go.uber.org/zap

## 用途与适用场景

Uber Go 的结构化日志库，以强类型字段记录日志。（[[zap-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get go.uber.org/zap`；示例使用 `go.uber.org/zap`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 项目组织索引：[[uber-go]]。
- uber-go 项目组织；个人创建者与当前维护名单待验证。
- 其他相关项目：[multierr](https://github.com/uber-go/multierr)、[fx](https://github.com/uber-go/fx)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
logger, err := zap.NewProduction()
if err != nil { log.Fatal(err) }
defer logger.Sync()
logger.Info("ready", zap.String("service", "api"))
```

## 关键限制

- NewProduction 默认 JSON 输出；Sync 在部分输出设备上可返回不影响日志的错误，按运行环境处理。

## 来源

- [[zap-go-official-research]]
- [官方仓库](https://github.com/uber-go/zap)；[Go Packages](https://pkg.go.dev/go.uber.org/zap)；[示例 API](https://pkg.go.dev/go.uber.org/zap)。
- 本地查阅记录：`raw/zap-go-official-research-2026-10-31.md`。
