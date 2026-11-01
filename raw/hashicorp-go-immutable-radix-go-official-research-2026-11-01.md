# github.com/hashicorp/go-immutable-radix/v2 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 的中文研究笔记，不是官方原文副本；代码片段尚未在本机运行。

## 官方来源

- 收件箱模块：`github.com/hashicorp/go-immutable-radix/v2`。
- [项目仓库](https://github.com/hashicorp/go-immutable-radix)；[所查 README 或仓库说明](https://raw.githubusercontent.com/hashicorp/go-immutable-radix/master/README.md)。
- [Go Packages 入口](https://pkg.go.dev/github.com/hashicorp/go-immutable-radix/v2)（具体 API 以目标版本为准）。
- 仓库归属账号：`hashicorp`；归属不等于个人创建者或现任维护者。

## 核心事实与用法

- 用途：提供泛型不可变 radix tree。
- 模块依赖：`go get github.com/hashicorp/go-immutable-radix/v2`。
- 官方资料中的用法线索或最小示意：

```go
tree := iradix.New[int](); tree, _, _ = tree.Insert([]byte("foo"), 1)
```

## 边界

- v2 引入泛型，与旧模块路径分开。
- 示例未在本机编译或运行；若为命令行工具，执行前核对目标版本的命令与参数。
- 创建者与现任维护者的具体身份待验证；不由仓库所有者直接推断。
