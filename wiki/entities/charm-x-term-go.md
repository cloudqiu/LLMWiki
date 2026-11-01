---
title: "github.com/charmbracelet/x/term"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/charm-x-term-go-official-research-2026-11-01.md]
---

# github.com/charmbracelet/x/term

## 用途与适用场景

跨平台查询终端大小、TTY 状态及原始模式。（[[charm-x-term-go-official-research]]）

## 依赖与版本

- 模块：`github.com/charmbracelet/x/term`；安装或依赖声明：`go get github.com/charmbracelet/x/term`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[charmbracelet]]：Charm 组织仓库；个人创建者与具体维护者待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```go
width, height, err := term.GetSize(os.Stdout.Fd()); _, _, _ = width, height, err
```

## 关键限制

- 需要有效终端文件描述符；x 仓库不承诺向后兼容。

## 来源

- [[charm-x-term-go-official-research]]；[官方仓库](https://github.com/charmbracelet/x)；[官方文档](https://pkg.go.dev/github.com/charmbracelet/x/term)。
- 本地查阅记录：`raw/charm-x-term-go-official-research-2026-11-01.md`。
