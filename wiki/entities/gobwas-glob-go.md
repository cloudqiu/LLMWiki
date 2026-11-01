---
title: "github.com/gobwas/glob"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/gobwas-glob-go-official-research-2026-11-01.md]
---

# github.com/gobwas/glob

## 用途与适用场景

编译并匹配 glob 模式。（[[gobwas-glob-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/gobwas/glob`；在项目中执行 `go get github.com/gobwas/glob`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 作者待验证；仓库归属账号不等于已核实的个人创建者。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
g, err := glob.Compile("*.go"); _ = g; _ = err
```

## 关键限制

- 模式语义不同于正则表达式。

## 来源

- [[gobwas-glob-go-official-research]]；[官方仓库](https://github.com/gobwas/glob)；[所查 README 或仓库说明](https://github.com/gobwas/glob)。
- 本地查阅记录：`raw/gobwas-glob-go-official-research-2026-11-01.md`。
