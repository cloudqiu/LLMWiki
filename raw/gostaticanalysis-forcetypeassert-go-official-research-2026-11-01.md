# github.com/gostaticanalysis/forcetypeassert 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 的中文研究笔记，不是官方原文副本；代码片段尚未在本机运行。

## 官方来源

- 收件箱模块：`github.com/gostaticanalysis/forcetypeassert`。
- [项目仓库](https://github.com/gostaticanalysis/forcetypeassert)；[所查 README 或仓库说明](https://raw.githubusercontent.com/gostaticanalysis/forcetypeassert/master/README.md)。
- [Go Packages 入口](https://pkg.go.dev/github.com/gostaticanalysis/forcetypeassert)（具体 API 以目标版本为准）。
- 仓库归属账号：`gostaticanalysis`；归属不等于个人创建者或现任维护者。

## 核心事实与用法

- 用途：检测未检查的 Go 类型断言。
- 模块依赖：`go get github.com/gostaticanalysis/forcetypeassert`。
- 官方资料中的用法线索或最小示意：

```sh
golangci-lint run --enable-only forcetypeassert ./...
```

## 边界

- 命令集成参数需按目标版本复核。
- 示例未在本机编译或运行；若为命令行工具，执行前核对目标版本的命令与参数。
- 创建者与现任维护者的具体身份待验证；不由仓库所有者直接推断。
