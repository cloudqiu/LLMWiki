# 4d63.com/gocheckcompilerdirectives 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`4d63.com/gocheckcompilerdirectives`。
- 官方模块：`4d63.com/gocheckcompilerdirectives`。
- 用途：检查 //go: 编译器指令注释是否有效，适合静态检查。
- [官方项目或文档](https://github.com/leighmcculloch/gocheckcompilerdirectives)；[Go Packages](https://pkg.go.dev/4d63.com/gocheckcompilerdirectives)。

## 安装与典型用法

```sh
go get 4d63.com/gocheckcompilerdirectives
```

在 golangci-lint v2 的配置中启用该 linter 后执行 `golangci-lint run`；这是集成使用，并非本模块的独立 CLI：

```yaml
linters:
  enable:
    - gocheckcompilerdirectives
```

## 身份与边界

- 身份：Leigh McCulloch 账号的项目；个人独立创建者与现任维护者待验证。
- 限制：官方 vanity 页只列模块与子包；独立 CLI 安装与调用方式待验证。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
