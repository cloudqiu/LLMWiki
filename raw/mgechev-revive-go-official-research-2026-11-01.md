# github.com/mgechev/revive 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/mgechev/revive`；核对路径：`github.com/mgechev/revive`。
- [官方仓库](https://github.com/mgechev/revive)；[所查 README 或仓库说明](https://raw.githubusercontent.com/mgechev/revive/master/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/mgechev/revive)。
- 依赖声明：`go get github.com/mgechev/revive`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 运行可配置的 Go lint 规则。

```sh
revive ./...
```

## 边界与待验证

- 规则可由 TOML 配置改变。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
