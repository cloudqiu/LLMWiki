---
title: "github.com/go-toolsmith/astequal"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/go-toolsmith-astequal-go-official-research-2026-11-01.md]
---

# github.com/go-toolsmith/astequal

## 用途与适用场景

比较 Go AST 结构是否相等。（[[go-toolsmith-astequal-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/go-toolsmith/astequal`；在项目中执行 `go get github.com/go-toolsmith/astequal`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 官方仓库归属账号：[[go-toolsmith]]；这只确认账号关联。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
same := astequal.Expr(strparse.Expr(`x`), strparse.Expr(`x`)); _ = same
```

## 关键限制

- 示例还需导入 strparse。

## 来源

- [[go-toolsmith-astequal-go-official-research]]；[官方仓库](https://github.com/go-toolsmith/astequal)；[所查 README 或仓库说明](https://github.com/go-toolsmith/astequal)。
- 本地查阅记录：`raw/go-toolsmith-astequal-go-official-research-2026-11-01.md`。
