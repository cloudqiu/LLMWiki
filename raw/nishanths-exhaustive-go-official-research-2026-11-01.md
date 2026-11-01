# github.com/nishanths/exhaustive 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/nishanths/exhaustive`；核对路径：`github.com/nishanths/exhaustive`。
- [官方仓库](https://github.com/nishanths/exhaustive)；[所查 README 或仓库说明](https://raw.githubusercontent.com/nishanths/exhaustive/master/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/nishanths/exhaustive)。
- 依赖声明：`go get github.com/nishanths/exhaustive`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 检查枚举型 switch 是否穷尽。

```sh
golangci-lint run --enable-only exhaustive ./...
```

## 边界与待验证

- 支持的 switch 类型和默认分支策略需配置。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
