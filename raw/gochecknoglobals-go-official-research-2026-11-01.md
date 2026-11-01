# 4d63.com/gochecknoglobals 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`4d63.com/gochecknoglobals`。
- 官方模块：`4d63.com/gochecknoglobals`。
- 用途：检测 Go 包级全局变量，帮助限制可变全局状态。
- [官方项目或文档](https://github.com/leighmcculloch/gochecknoglobals)；[Go Packages](https://pkg.go.dev/4d63.com/gochecknoglobals)。

## 安装与典型用法

```sh
go install 4d63.com/gochecknoglobals@latest
```

```sh
gochecknoglobals ./...
```

## 身份与边界

- 身份：Leigh McCulloch 账号的项目；个人独立创建者与现任维护者待验证。
- 限制：静态规则有特定豁免；应对照项目 README 和实际代码判断误报。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
