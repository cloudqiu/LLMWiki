# github.com/charmbracelet/x/windows 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/charmbracelet/x/windows`；官方模块：`github.com/charmbracelet/x/windows`。
- 用途：封装 Charm 所需的 Windows Console 输入记录与系统调用。
- [项目官方仓库](https://github.com/charmbracelet/x)；[所查官方文档](https://github.com/charmbracelet/x/tree/main/windows)；[Go Packages](https://pkg.go.dev/github.com/charmbracelet/x/windows)。
- [账号或组织主页](https://github.com/charmbracelet)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/charmbracelet/x/windows
```

```go
在 Windows 专用 Go 文件中使用 windows.InputRecord 表示控制台输入记录
```

## 边界

- 仅 Windows 构建可用；目前未核实可脱离 Charm 终端栈的最小完整运行示例。 Windows 专用示意，需位于带 //go:build windows 的文件，非完整程序。
- 版本由目标项目锁定；示例未在本机下载或编译。
