# github.com/tommy-muehle/go-mnd/v2 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 中文研究笔记，不是官方原文副本；示例未在本机运行。

## 路径与来源

- 收件箱原条目：`github.com/tommy-muehle/go-mnd/v2`；核实后的路径：`github.com/tommy-muehle/go-mnd/v2`。
- [官方仓库](https://github.com/tommy-muehle/go-mnd)；[所查 README 或版本文档](https://github.com/tommy-muehle/go-mnd)；[Go Packages 入口](https://pkg.go.dev/github.com/tommy-muehle/go-mnd/v2)。
- 在 Go 项目中声明依赖：`go get github.com/tommy-muehle/go-mnd/v2`。
- 仓库账号可确认项目关联；具体个人创建者与现任维护者待验证。

## 用途与典型用法

- 检测 Go 代码中的魔法数字。

```sh
golangci-lint run --enable-only mnd ./...
```

## 边界与待验证

- 数字常量的可接受性依赖上下文和规则配置。
- 示例未在本机编译或运行；按目标项目版本复核参数与 API。
