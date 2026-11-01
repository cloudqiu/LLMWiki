---
title: "github.com/alingse/asasalint"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/asasalint-go-official-research-2026-11-01.md]
---

# github.com/alingse/asasalint

## 用途与适用场景

找出把 any slice 错误地作为单个 any 传入可变参数函数的情况。（[[asasalint-go-official-research]]）

## 依赖与版本

- 模块：`github.com/alingse/asasalint`；安装或依赖声明：`go install github.com/alingse/asasalint/cmd/asasalint@latest`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- 仓库账号 alingse；个人创建者和当前维护者待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```text
asasalint ./...
```

## 关键限制

- 可用 -e 排除有意使用的函数；需结合项目代码判断。

## 来源

- [[asasalint-go-official-research]]；[官方资料](https://github.com/alingse/asasalint)；[Go Packages](https://pkg.go.dev/github.com/alingse/asasalint)。
- 本地研究笔记：`raw/asasalint-go-official-research-2026-11-01.md`。
