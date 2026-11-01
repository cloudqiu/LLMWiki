---
title: "github.com/charmbracelet/x/termios"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/charm-x-termios-go-official-research-2026-11-01.md]
---

# github.com/charmbracelet/x/termios

## 用途与适用场景

在 Unix 终端读取或设置 termios 与窗口尺寸。（[[charm-x-termios-go-official-research]]）

## 依赖与版本

- 模块：`github.com/charmbracelet/x/termios`；安装或依赖声明：`go get github.com/charmbracelet/x/termios`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[charmbracelet]]：Charm 组织仓库；个人创建者与具体维护者待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```go
winsize, err := termios.GetWinsize(int(os.Stdout.Fd())); _, _ = winsize, err
```

## 关键限制

- 面向支持 termios 的系统；不适用于 Windows；x 仓库不承诺向后兼容。

## 来源

- [[charm-x-termios-go-official-research]]；[官方仓库](https://github.com/charmbracelet/x)；[官方文档](https://pkg.go.dev/github.com/charmbracelet/x/termios)。
- 本地查阅记录：`raw/charm-x-termios-go-official-research-2026-11-01.md`。
