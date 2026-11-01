---
title: "github.com/ashanbrown/makezero/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/makezero-v2-go-official-research-2026-11-01.md]
---

# github.com/ashanbrown/makezero/v2

## 用途与适用场景

检查先创建非零长度 slice 又 append 导致多出零值元素。（[[makezero-v2-go-official-research]]）

## 依赖与版本

- 模块：`github.com/ashanbrown/makezero/v2`；安装或依赖声明：`go install github.com/ashanbrown/makezero/v2@latest`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- 仓库账号 ashanbrown；个人创建者和当前维护者待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```text
makezero ./...
```

## 关键限制

- 默认仅报告后续 append 的相关模式；-always 会扩大检查范围。

## 来源

- [[makezero-v2-go-official-research]]；[官方资料](https://pkg.go.dev/github.com/ashanbrown/makezero/v2)；[Go Packages](https://pkg.go.dev/github.com/ashanbrown/makezero/v2)。
- 本地研究笔记：`raw/makezero-v2-go-official-research-2026-11-01.md`。
