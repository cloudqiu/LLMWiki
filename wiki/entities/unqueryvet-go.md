---
title: "github.com/MirrexOne/unqueryvet"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/unqueryvet-go-official-research-2026-11-01.md]
---

# github.com/MirrexOne/unqueryvet

## 用途与适用场景

检查 SQL 查询中 SELECT * 等不显式选列的写法。（[[unqueryvet-go-official-research]]）

## 依赖与版本

- 模块：`github.com/MirrexOne/unqueryvet`；安装或依赖声明：`go install github.com/MirrexOne/unqueryvet/cmd/unqueryvet@latest`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- 仓库账号 MirrexOne；个人创建者和当前维护者待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```text
unqueryvet ./...
```

## 关键限制

- 主要识别静态可分析的 SQL 字符串；动态拼接覆盖范围待验证。

## 来源

- [[unqueryvet-go-official-research]]；[官方资料](https://github.com/MirrexOne/unqueryvet)；[Go Packages](https://pkg.go.dev/github.com/MirrexOne/unqueryvet)。
- 本地研究笔记：`raw/unqueryvet-go-official-research-2026-11-01.md`。
