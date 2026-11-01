---
title: "dev.gaijin.team/go/exhaustruct/v5"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/exhaustruct-v5-go-official-research-2026-11-01.md]
---

# dev.gaijin.team/go/exhaustruct/v5

## 用途与适用场景

检查结构体字面量是否显式初始化全部字段。（[[exhaustruct-v5-go-official-research]]）

## 依赖与版本

- 官方模块：`dev.gaijin.team/go/exhaustruct/v5`。
- 安装或依赖声明：`go install dev.gaijin.team/go/exhaustruct/v5/cmd/exhaustruct@latest`。
- 查阅日期：2026-11-01；具体版本以目标项目锁定为准。

## 作者与维护者

- [[gaijin-entertainment]]；Gaijin Entertainment 组织仓库；个人创建者及具体维护者待验证。

## 典型用法

下面示例以官方文档或项目 README 为依据；**未在本机运行**。命令需在适当 Go 项目中执行；Go 代码片段需补齐 import 与外围函数。

```sh
exhaustruct ./...
```

## 关键限制

- 可能与有意省略零值字段的风格冲突；v5 路径不可与旧主版本混用。

## 来源

- [[exhaustruct-v5-go-official-research]]；[官方项目或文档](https://github.com/GaijinEntertainment/go-exhaustruct)；[Go Packages](https://pkg.go.dev/dev.gaijin.team/go/exhaustruct/v5)。
- 本地原始资料：`raw/exhaustruct-v5-go-official-research-2026-11-01.md`。
