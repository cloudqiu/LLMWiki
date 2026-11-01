# github.com/charmbracelet/ultraviolet 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/charmbracelet/ultraviolet`；官方模块：`github.com/charmbracelet/ultraviolet`。
- 用途：提供终端 UI 的 cell 绘制、输入和差量渲染原语。
- [项目官方仓库](https://github.com/charmbracelet/ultraviolet)；[所查官方文档](https://github.com/charmbracelet/ultraviolet)；[Go Packages](https://pkg.go.dev/github.com/charmbracelet/ultraviolet)。
- [账号或组织主页](https://github.com/charmbracelet)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/charmbracelet/ultraviolet@latest
```

```go
terminal := uv.DefaultTerminal(); screen := terminal.Screen(); _ = screen
```

## 边界

- 完整交互需 Start/Stop 和事件循环；示例只是初始化片段。
- 版本由目标项目锁定；示例未在本机下载或编译。
