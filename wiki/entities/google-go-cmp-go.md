---
title: "github.com/google/go-cmp"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/google-go-cmp-go-official-research-2026-11-01.md]
---

# github.com/google/go-cmp

## 用途与适用场景

比较 Go 值并给出结构化差异。（[[google-go-cmp-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/google/go-cmp`；在项目中执行 `go get github.com/google/go-cmp`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 官方仓库归属账号：[[google-org]]；这只确认账号关联。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
diff := cmp.Diff(want, got); _ = diff
```

## 关键限制

- 比较未导出字段通常需要显式选项。

## 来源

- [[google-go-cmp-go-official-research]]；[官方仓库](https://github.com/google/go-cmp)；[所查 README 或仓库说明](https://raw.githubusercontent.com/google/go-cmp/master/README.md)。
- 本地查阅记录：`raw/google-go-cmp-go-official-research-2026-11-01.md`。
