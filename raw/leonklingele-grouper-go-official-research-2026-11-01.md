# github.com/leonklingele/grouper 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 研究笔记，并非官方原文副本；示例未在本机运行。

## 路径与官方来源

- 收件箱原条目：`github.com/leonklingele/grouper`；核对路径：`github.com/leonklingele/grouper`。
- [官方仓库](https://github.com/leonklingele/grouper)；[所查 README 或仓库说明](https://raw.githubusercontent.com/leonklingele/grouper/master/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/leonklingele/grouper)。
- 依赖声明：`go get github.com/leonklingele/grouper`。
- 仓库账号归属可由页面确认；具体创建者和现任维护者待验证。

## 用途与典型用法

- 检查 import、const、var 声明分组。

```sh
grouper -import-require-single-import -import-require-grouping ./...
```

## 边界与待验证

- 组别规则由标志决定。
- 代码或命令未在本机编译或运行；按目标项目锁定的版本复核。
