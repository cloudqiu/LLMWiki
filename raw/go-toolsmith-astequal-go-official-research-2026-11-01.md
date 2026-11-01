# github.com/go-toolsmith/astequal 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 的中文研究笔记，不是官方原文副本；代码片段尚未在本机运行。

## 官方来源

- 收件箱模块：`github.com/go-toolsmith/astequal`。
- [项目仓库](https://github.com/go-toolsmith/astequal)；[所查 README 或仓库说明](https://github.com/go-toolsmith/astequal)。
- [Go Packages 入口](https://pkg.go.dev/github.com/go-toolsmith/astequal)（具体 API 以目标版本为准）。
- 仓库归属账号：`go-toolsmith`；归属不等于个人创建者或现任维护者。

## 核心事实与用法

- 用途：比较 Go AST 结构是否相等。
- 模块依赖：`go get github.com/go-toolsmith/astequal`。
- 官方资料中的用法线索或最小示意：

```go
same := astequal.Expr(strparse.Expr(`x`), strparse.Expr(`x`)); _ = same
```

## 边界

- 示例还需导入 strparse。
- 示例未在本机编译或运行；若为命令行工具，执行前核对目标版本的命令与参数。
- 创建者与现任维护者的具体身份待验证；不由仓库所有者直接推断。
