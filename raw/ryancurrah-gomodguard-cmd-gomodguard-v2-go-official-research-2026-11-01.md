# github.com/ryancurrah/gomodguard/cmd/gomodguard/v2 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 中文研究笔记，不是官方原文副本；示例未在本机运行。

## 路径与来源

- 收件箱原条目：`github.com/ryancurrah/gomodguard/v2`；核实后的路径：`github.com/ryancurrah/gomodguard/cmd/gomodguard/v2`。
- [官方仓库](https://github.com/ryancurrah/gomodguard)；[所查 README 或版本文档](https://raw.githubusercontent.com/ryancurrah/gomodguard/main/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/ryancurrah/gomodguard/cmd/gomodguard/v2)。
- v2 命令为仓库内独立子模块；安装：`go install github.com/ryancurrah/gomodguard/cmd/gomodguard/v2@latest`。
- 仓库账号可确认项目关联；具体个人创建者与现任维护者待验证。

## 用途与典型用法

- 按允许和禁止清单检查 Go 模块依赖。

```sh
gomodguard ./...
```

## 边界与待验证

- 收件箱写作仓库根路径 /v2；官方 v2 CLI 实际是 cmd/gomodguard/v2 子模块，规则来自 .gomodguard.yaml。
- 示例未在本机编译或运行；按目标项目版本复核参数与 API。
