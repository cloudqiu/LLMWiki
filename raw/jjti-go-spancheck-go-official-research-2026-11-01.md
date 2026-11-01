# github.com/jjti/go-spancheck 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/jjti/go-spancheck`；核对路径：`github.com/jjti/go-spancheck`。
- [官方仓库](https://github.com/jjti/go-spancheck)；[所查 README 或仓库说明](https://raw.githubusercontent.com/jjti/go-spancheck/main/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/jjti/go-spancheck)。
- 依赖声明：`go get github.com/jjti/go-spancheck`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 检查追踪 span 是否正确结束及设置状态。

```sh
spancheck -checks 'end,set-status,record-error' ./...
```

## 边界与待验证

- 对 OpenTelemetry 与 OpenCensus 的支持按目标版本核对。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
