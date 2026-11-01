# github.com/charmbracelet/x/term 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/charmbracelet/x/term`；官方模块：`github.com/charmbracelet/x/term`。
- 用途：跨平台查询终端大小、TTY 状态及原始模式。
- [项目官方仓库](https://github.com/charmbracelet/x)；[所查官方文档](https://pkg.go.dev/github.com/charmbracelet/x/term)；[Go Packages](https://pkg.go.dev/github.com/charmbracelet/x/term)。
- [账号或组织主页](https://github.com/charmbracelet)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/charmbracelet/x/term
```

```go
width, height, err := term.GetSize(os.Stdout.Fd()); _, _, _ = width, height, err
```

## 边界

- 需要有效终端文件描述符；x 仓库不承诺向后兼容。
- 版本由目标项目锁定；示例未在本机下载或编译。
