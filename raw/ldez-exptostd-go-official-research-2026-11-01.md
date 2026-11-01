# github.com/ldez/exptostd 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/ldez/exptostd`；核对路径：`github.com/ldez/exptostd`。
- [官方仓库](https://github.com/ldez/exptostd)；[所查 README 或仓库说明](https://github.com/ldez/exptostd)；[Go Packages 入口](https://pkg.go.dev/github.com/ldez/exptostd)。
- 依赖声明：`go get github.com/ldez/exptostd`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 检测可由标准库替代的 x/exp API。

```sh
golangci-lint run --enable-only exptostd ./...
```

## 边界与待验证

- 可替代 API 取决于 Go 版本。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
