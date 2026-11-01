# github.com/golangci/golangci-lint/v2 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`github.com/golangci/golangci-lint/v2`。
- 官方模块：`github.com/golangci/golangci-lint/v2`。
- 用途：聚合多种 Go linter 并统一配置、运行，适合项目和 CI。
- [官方项目或文档](https://golangci-lint.run/docs/welcome/install/local/)；[Go Packages](https://pkg.go.dev/github.com/golangci/golangci-lint/v2)。

## 安装与典型用法

```sh
go install github.com/golangci/golangci-lint/v2/cmd/golangci-lint@v2.15.0
```

```sh
golangci-lint run
```

## 身份与边界

- 身份：golangci 组织发布；最初创建者及当前具体维护人员待验证。
- 限制：v2 配置与 v1 不完全兼容；升级须核对迁移文档。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
