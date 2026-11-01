# github.com/raeperd/recvcheck 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/raeperd/recvcheck`；核对路径：`github.com/raeperd/recvcheck`。
- [官方仓库](https://github.com/raeperd/recvcheck)；[所查 README 或仓库说明](https://raw.githubusercontent.com/raeperd/recvcheck/main/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/raeperd/recvcheck)。
- 依赖声明：`go get github.com/raeperd/recvcheck`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 检查 Go 方法是否混用指针和值接收者。

```sh
golangci-lint run --enable-only recvcheck ./...
```

## 边界与待验证

- 混用可能有设计原因，需结合类型语义判断。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
