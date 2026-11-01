---
title: "github.com/daixiang0/gci"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/gci-go-official-research-2026-11-01.md]
---

# github.com/daixiang0/gci

## 用途与适用场景

按可配置分组确定性整理 Go import，适合代码风格检查。（[[gci-go-official-research]]）

## 依赖与版本

- 官方模块：`github.com/daixiang0/gci`。
- 安装或依赖声明：`go install github.com/daixiang0/gci@latest`。
- 查阅日期：2026-11-01；具体版本以目标项目锁定为准。

## 作者与维护者

- 仓库属于 daixiang0；个人创建者与当前维护者待验证。

## 典型用法

下面示例以官方文档或项目 README 为依据；**未在本机运行**。命令需在适当 Go 项目中执行；Go 代码片段需补齐 import 与外围函数。

```sh
gci write -s standard -s default main.go
```

## 关键限制

- write 会原地改文件；先用 gci diff main.go 预览。

## 来源

- [[gci-go-official-research]]；[官方项目或文档](https://github.com/daixiang0/gci)；[Go Packages](https://pkg.go.dev/github.com/daixiang0/gci)。
- 本地原始资料：`raw/gci-go-official-research-2026-11-01.md`。
