---
title: "charm.land/lipgloss/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/lipgloss-v2-go-official-research-2026-11-01.md]
---

# charm.land/lipgloss/v2

## 用途与适用场景

为终端 UI 文本和布局声明样式，适合 Charm 生态 TUI。（[[lipgloss-v2-go-official-research]]）

## 依赖与版本

- 官方模块：`charm.land/lipgloss/v2`。
- 安装或依赖声明：`go get charm.land/lipgloss/v2`。
- 查阅日期：2026-11-01；具体版本以目标项目锁定为准。

## 作者与维护者

- [[charmbracelet]]；Charmbracelet 组织维护；具体个人创建者待验证。

## 典型用法

下面示例以官方文档或项目 README 为依据；**未在本机运行**。命令需在适当 Go 项目中执行；Go 代码片段需补齐 import 与外围函数。

```go
style := lipgloss.NewStyle().Bold(true)
fmt.Println(style.Render("Hello"))
```

## 关键限制

- v2 使用新模块路径；不能直接沿用 v1 的 import。

## 来源

- [[lipgloss-v2-go-official-research]]；[官方项目或文档](https://github.com/charmbracelet/lipgloss)；[Go Packages](https://pkg.go.dev/charm.land/lipgloss/v2)。
- 本地原始资料：`raw/lipgloss-v2-go-official-research-2026-11-01.md`。
