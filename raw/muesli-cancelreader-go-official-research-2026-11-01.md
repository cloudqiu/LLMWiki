# github.com/muesli/cancelreader 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/muesli/cancelreader`；核对路径：`github.com/muesli/cancelreader`。
- [官方仓库](https://github.com/muesli/cancelreader)；[所查 README 或仓库说明](https://raw.githubusercontent.com/muesli/cancelreader/master/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/muesli/cancelreader)。
- 依赖声明：`go get github.com/muesli/cancelreader`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 为 io.Reader 提供可取消读取包装。

```go
reader, err := cancelreader.NewReader(file); _, _ = reader, err
```

## 边界与待验证

- 非文件 Reader 的 Cancel 行为受官方说明限制。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
