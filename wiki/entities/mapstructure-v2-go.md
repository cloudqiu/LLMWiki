---
title: "github.com/go-viper/mapstructure/v2"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/mapstructure-v2-go-official-research-2026-10-31.md]
---

# github.com/go-viper/mapstructure/v2

## 用途与适用场景

将 map 解码到 Go struct，常用于配置处理。（[[mapstructure-v2-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/go-viper/mapstructure/v2`；示例使用 `github.com/go-viper/mapstructure/v2`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 项目组织索引：[[go-viper]]。
- go-viper 社区维护分支；个人创建及维护角色待验证。
- 其他相关项目：[encoding](https://github.com/go-viper/encoding)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
var cfg struct { Port int `mapstructure:"port"` }
err := mapstructure.Decode(map[string]any{"port": 8080}, &cfg)
fmt.Println(cfg.Port, err)
```

## 关键限制

- 默认 Decode 不等于输入校验；未知字段要配置 ErrorUnused。v2 为 go-viper 分支，勿与原 v1 混用。

## 来源

- [[mapstructure-v2-go-official-research]]
- [官方仓库](https://github.com/go-viper/mapstructure)；[Go Packages](https://pkg.go.dev/github.com/go-viper/mapstructure/v2)；[示例 API](https://pkg.go.dev/github.com/go-viper/mapstructure/v2)。
- 本地查阅记录：`raw/mapstructure-v2-go-official-research-2026-10-31.md`。
