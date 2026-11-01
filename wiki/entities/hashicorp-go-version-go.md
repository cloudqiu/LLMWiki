---
title: "github.com/hashicorp/go-version"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/hashicorp-go-version-go-official-research-2026-11-01.md]
---

# github.com/hashicorp/go-version

## 用途与适用场景

解析和比较语义版本及约束。（[[hashicorp-go-version-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/hashicorp/go-version`；在项目中执行 `go get github.com/hashicorp/go-version`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 官方仓库归属账号：[[hashicorp]]；这只确认账号关联。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
v, err := version.NewVersion("1.2.3"); _ = v; _ = err
```

## 关键限制

- 版本输入需符合项目支持的 SemVer 形式。

## 来源

- [[hashicorp-go-version-go-official-research]]；[官方仓库](https://github.com/hashicorp/go-version)；[所查 README 或仓库说明](https://raw.githubusercontent.com/hashicorp/go-version/main/README.md)。
- 本地查阅记录：`raw/hashicorp-go-version-go-official-research-2026-11-01.md`。
