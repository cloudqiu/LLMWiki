# github.com/xen0n/gosmopolitan 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 中文研究笔记，不是官方原文副本；示例未在本机运行。

## 路径与来源

- 收件箱原条目：`github.com/xen0n/gosmopolitan`；核实后的路径：`github.com/xen0n/gosmopolitan`。
- [官方仓库](https://github.com/xen0n/gosmopolitan)；[所查 README 或版本文档](https://github.com/xen0n/gosmopolitan)；[Go Packages 入口](https://pkg.go.dev/github.com/xen0n/gosmopolitan)。
- 在 Go 项目中声明依赖：`go get github.com/xen0n/gosmopolitan`。
- 仓库账号可确认项目关联；具体个人创建者与现任维护者待验证。

## 用途与典型用法

- 检查可能妨碍国际化和本地化的 Go 代码模式。

```sh
golangci-lint run --enable-only gosmopolitan ./...
```

## 边界与待验证

- 规则特别针对非拉丁文字和本地时区用法，不适合所有项目。
- 示例未在本机编译或运行；按目标项目版本复核参数与 API。
