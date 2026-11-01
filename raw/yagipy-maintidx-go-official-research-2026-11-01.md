# github.com/yagipy/maintidx 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 中文研究笔记，不是官方原文副本；示例未在本机运行。

## 路径与来源

- 收件箱原条目：`github.com/yagipy/maintidx`；核实后的路径：`github.com/yagipy/maintidx`。
- [官方仓库](https://github.com/yagipy/maintidx)；[所查 README 或版本文档](https://raw.githubusercontent.com/yagipy/maintidx/master/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/yagipy/maintidx)。
- 在 Go 项目中声明依赖：`go get github.com/yagipy/maintidx`。
- 仓库账号可确认项目关联；具体个人创建者与现任维护者待验证。

## 用途与典型用法

- 计算 Go 函数的 maintainability index。

```sh
golangci-lint run --enable-only maintidx ./...
```

## 边界与待验证

- 指标为实验性度量，不应单独决定代码质量。
- 示例未在本机编译或运行；按目标项目版本复核参数与 API。
