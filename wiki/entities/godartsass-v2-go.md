---
title: "github.com/bep/godartsass/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/godartsass-v2-go-official-research-2026-11-01.md]
---

# github.com/bep/godartsass/v2

## 用途与适用场景

通过 Dart Sass Embedded 协议从 Go 编译 Sass/SCSS。（[[godartsass-v2-go-official-research]]）

## 依赖与版本

- 模块：`github.com/bep/godartsass/v2`；安装或依赖声明：`go get github.com/bep/godartsass/v2`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- [[bjorn-erik-pedersen]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```go
t, err := godartsass.Start(godartsass.Options{}); _ = t; _ = err
```

## 关键限制

- 需可用的 sass --embedded 可执行文件；v2 对应 Embedded 协议 v2。

## 来源

- [[godartsass-v2-go-official-research]]；[官方资料](https://pkg.go.dev/github.com/bep/godartsass/v2)；[Go Packages](https://pkg.go.dev/github.com/bep/godartsass/v2)。
- 本地研究笔记：`raw/godartsass-v2-go-official-research-2026-11-01.md`。
