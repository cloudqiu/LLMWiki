---
title: "github.com/alexkohler/nakedret/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/nakedret-v2-go-official-research-2026-11-01.md]
---

# github.com/alexkohler/nakedret/v2

## 用途与适用场景

找出超过长度阈值的函数里的裸 return。（[[nakedret-v2-go-official-research]]）

## 依赖与版本

- 模块：`github.com/alexkohler/nakedret/v2`；安装或依赖声明：`go install github.com/alexkohler/nakedret/v2/cmd/nakedret@latest`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- 仓库账号 alexkohler；个人创建者和当前维护者待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```text
nakedret ./...
```

## 关键限制

- 阈值是风格选择；应在项目中统一配置。

## 来源

- [[nakedret-v2-go-official-research]]；[官方资料](https://github.com/alexkohler/nakedret)；[Go Packages](https://pkg.go.dev/github.com/alexkohler/nakedret/v2)。
- 本地研究笔记：`raw/nakedret-v2-go-official-research-2026-11-01.md`。
