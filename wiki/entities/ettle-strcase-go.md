---
title: "github.com/ettle/strcase"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/ettle-strcase-go-official-research-2026-11-01.md]
---

# github.com/ettle/strcase

## 用途与适用场景

转换 snake_case、camelCase 等命名形式。（[[ettle-strcase-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/ettle/strcase`；在项目中执行 `go get github.com/ettle/strcase`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 作者待验证；仓库归属账号不等于已核实的个人创建者。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
s := strcase.ToSnake("Hello World"); _ = s
```

## 关键限制

- 初始缩写和 Unicode 行为按实际输入验证。

## 来源

- [[ettle-strcase-go-official-research]]；[官方仓库](https://github.com/ettle/strcase)；[所查 README 或仓库说明](https://github.com/ettle/strcase)。
- 本地查阅记录：`raw/ettle-strcase-go-official-research-2026-11-01.md`。
