# github.com/daixiang0/gci 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`github.com/daixiang0/gci`。
- 官方模块：`github.com/daixiang0/gci`。
- 用途：按可配置分组确定性整理 Go import，适合代码风格检查。
- [官方项目或文档](https://github.com/daixiang0/gci)；[Go Packages](https://pkg.go.dev/github.com/daixiang0/gci)。

## 安装与典型用法

```sh
go install github.com/daixiang0/gci@latest
```

```sh
gci write -s standard -s default main.go
```

## 身份与边界

- 身份：仓库属于 daixiang0；个人创建者与当前维护者待验证。
- 限制：write 会原地改文件；先用 gci diff main.go 预览。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
