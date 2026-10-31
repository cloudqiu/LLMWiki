---
title: "github.com/rs/zerolog"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/zerolog-go-official-research-2026-10-31.md]
---

# github.com/rs/zerolog

## 用途与适用场景

链式 API 输出结构化 JSON 日志，适合低分配的服务日志。（[[zerolog-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/rs/zerolog`；示例使用 `github.com/rs/zerolog`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 作者索引：[[olivier-poitrey]]。
- 项目账号 rs；个人创建者姓名与独立维护角色待验证。
- 其他相关项目：[cors](https://github.com/rs/cors)、[xid](https://github.com/rs/xid)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
logger := zerolog.New(os.Stdout).With().Timestamp().Logger()
logger.Info().Str("service", "api").Msg("ready")
```

## 关键限制

- 事件对象短暂复用，不应持有；并发修改 logger context 应遵循文档约束。

## 来源

- [[zerolog-go-official-research]]
- [官方仓库](https://github.com/rs/zerolog)；[Go Packages](https://pkg.go.dev/github.com/rs/zerolog)；[示例 API](https://pkg.go.dev/github.com/rs/zerolog)。
- 本地查阅记录：`raw/zerolog-go-official-research-2026-10-31.md`。
