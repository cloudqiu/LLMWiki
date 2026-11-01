---
title: "github.com/Masterminds/semver/v3"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/masterminds-semver-v3-go-official-research-2026-11-01.md]
---

# github.com/Masterminds/semver/v3

## 用途与适用场景

解析 Semantic Version 并检验版本约束。（[[masterminds-semver-v3-go-official-research]]）

## 依赖与版本

- 模块：`github.com/Masterminds/semver/v3`；安装或依赖声明：`go get github.com/Masterminds/semver/v3`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- 仓库账号 Masterminds；个人创建者和当前维护者待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```go
c, _ := semver.NewConstraint(">= 1.2.3"); v, _ := semver.NewVersion("1.3.0"); ok := c.Check(v); _ = ok
```

## 关键限制

- 预发布版本和 ASCII 排序有专门语义，不能按普通字符串比较理解。

## 来源

- [[masterminds-semver-v3-go-official-research]]；[官方资料](https://github.com/Masterminds/semver)；[Go Packages](https://pkg.go.dev/github.com/Masterminds/semver/v3)。
- 本地研究笔记：`raw/masterminds-semver-v3-go-official-research-2026-11-01.md`。
