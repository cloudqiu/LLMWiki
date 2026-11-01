---
title: "github.com/charmbracelet/ultraviolet"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/ultraviolet-go-official-research-2026-11-01.md]
---

# github.com/charmbracelet/ultraviolet

## 用途与适用场景

提供终端 UI 的 cell 绘制、输入和差量渲染原语。（[[ultraviolet-go-official-research]]）

## 依赖与版本

- 模块：`github.com/charmbracelet/ultraviolet`；安装或依赖声明：`go get github.com/charmbracelet/ultraviolet@latest`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[charmbracelet]]：Charm 组织仓库；个人创建者与具体维护者待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```go
terminal := uv.DefaultTerminal(); screen := terminal.Screen(); _ = screen
```

## 关键限制

- 完整交互需 Start/Stop 和事件循环；示例只是初始化片段。

## 来源

- [[ultraviolet-go-official-research]]；[官方仓库](https://github.com/charmbracelet/ultraviolet)；[官方文档](https://github.com/charmbracelet/ultraviolet)。
- 本地查阅记录：`raw/ultraviolet-go-official-research-2026-11-01.md`。
