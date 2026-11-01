# charm.land/lipgloss/v2 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`charm.land/lipgloss/v2`。
- 官方模块：`charm.land/lipgloss/v2`。
- 用途：为终端 UI 文本和布局声明样式，适合 Charm 生态 TUI。
- [官方项目或文档](https://github.com/charmbracelet/lipgloss)；[Go Packages](https://pkg.go.dev/charm.land/lipgloss/v2)。

## 安装与典型用法

```go
go get charm.land/lipgloss/v2
```

```go
style := lipgloss.NewStyle().Bold(true)
fmt.Println(style.Render("Hello"))
```

## 身份与边界

- 身份：Charmbracelet 组织维护；具体个人创建者待验证。
- 限制：v2 使用新模块路径；不能直接沿用 v1 的 import。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
