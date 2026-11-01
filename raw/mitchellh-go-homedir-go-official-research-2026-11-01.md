# github.com/mitchellh/go-homedir 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/mitchellh/go-homedir`；核对路径：`github.com/mitchellh/go-homedir`。
- [官方仓库](https://github.com/mitchellh/go-homedir)；[所查 README 或仓库说明](https://raw.githubusercontent.com/mitchellh/go-homedir/master/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/mitchellh/go-homedir)。
- 依赖声明：`go get github.com/mitchellh/go-homedir`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 在无 cgo 情况下获取和展开当前用户主目录。

```go
dir, err := homedir.Dir(); _, _ = dir, err
```

## 边界与待验证

- 只针对当前用户的主目录。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
