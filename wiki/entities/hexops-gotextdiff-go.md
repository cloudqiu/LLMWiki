---
title: "github.com/hexops/gotextdiff"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/hexops-gotextdiff-go-official-research-2026-11-01.md]
---

# github.com/hexops/gotextdiff

## 用途与适用场景

用 Go 生成统一格式文本差异。（[[hexops-gotextdiff-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/hexops/gotextdiff`；项目中执行 `go get github.com/hexops/gotextdiff`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```go
edits := myers.ComputeEdits(uri, before, after); _ = edits
```

## 关键限制

- 差异算法基于文本编辑，文件 URI 与换行需按调用场景处理。

## 来源

- [[hexops-gotextdiff-go-official-research]]；[官方仓库](https://github.com/hexops/gotextdiff)；[所查 README 或仓库说明](https://raw.githubusercontent.com/hexops/gotextdiff/main/README.md)。
- 本地笔记：`raw/hexops-gotextdiff-go-official-research-2026-11-01.md`。
