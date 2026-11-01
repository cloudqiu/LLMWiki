---
title: "github.com/charmbracelet/x/ansi"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/charm-x-ansi-go-official-research-2026-11-01.md]
---

# github.com/charmbracelet/x/ansi

## 用途与适用场景

解析、生成和清理 ANSI 终端控制序列。（[[charm-x-ansi-go-official-research]]）

## 依赖与版本

- 模块：`github.com/charmbracelet/x/ansi`；安装或依赖声明：`go get github.com/charmbracelet/x/ansi`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[charmbracelet]]：Charm 组织仓库；个人创建者与具体维护者待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```go
clean := ansi.Strip("\x1b[31mred\x1b[0m"); _ = clean
```

## 关键限制

- x 仓库是实验性项目，不承诺向后兼容。

## 来源

- [[charm-x-ansi-go-official-research]]；[官方仓库](https://github.com/charmbracelet/x)；[官方文档](https://pkg.go.dev/github.com/charmbracelet/x/ansi)。
- 本地查阅记录：`raw/charm-x-ansi-go-official-research-2026-11-01.md`。
