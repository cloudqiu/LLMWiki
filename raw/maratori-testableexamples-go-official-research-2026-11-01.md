# github.com/maratori/testableexamples 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/maratori/testableexemples`；核对路径：`github.com/maratori/testableexamples`。
- [官方仓库](https://github.com/maratori/testableexamples)；[所查 README 或仓库说明](https://github.com/maratori/testableexamples)；[Go Packages 入口](https://pkg.go.dev/github.com/maratori/testableexamples)。
- 依赖声明：`go get github.com/maratori/testableexamples`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 检查 Go Example 是否声明可验证输出。

```sh
golangci-lint run --enable-only testableexamples ./...
```

## 边界与待验证

- 只保证示例可被测试框架验证，不保证示例质量。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
