---
title: "github.com/charmbracelet/x/windows"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/charm-x-windows-go-official-research-2026-11-01.md]
---

# github.com/charmbracelet/x/windows

## 用途与适用场景

封装 Charm 所需的 Windows Console 输入记录与系统调用。（[[charm-x-windows-go-official-research]]）

## 依赖与版本

- 模块：`github.com/charmbracelet/x/windows`；安装或依赖声明：`go get github.com/charmbracelet/x/windows`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[charmbracelet]]：Charm 组织仓库；个人创建者与具体维护者待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```go
在 Windows 专用 Go 文件中使用 windows.InputRecord 表示控制台输入记录
```

## 关键限制

- 仅 Windows 构建可用；目前未核实可脱离 Charm 终端栈的最小完整运行示例。 Windows 专用示意，需位于带 //go:build windows 的文件，非完整程序。

## 来源

- [[charm-x-windows-go-official-research]]；[官方仓库](https://github.com/charmbracelet/x)；[官方文档](https://github.com/charmbracelet/x/tree/main/windows)。
- 本地查阅记录：`raw/charm-x-windows-go-official-research-2026-11-01.md`。
