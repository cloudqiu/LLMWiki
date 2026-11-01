# dev.gaijin.team/go/exhaustruct/v5 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`dev.gaijin.team/go/exhaustruct/v5`。
- 官方模块：`dev.gaijin.team/go/exhaustruct/v5`。
- 用途：检查结构体字面量是否显式初始化全部字段。
- [官方项目或文档](https://github.com/GaijinEntertainment/go-exhaustruct)；[Go Packages](https://pkg.go.dev/dev.gaijin.team/go/exhaustruct/v5)。

## 安装与典型用法

```sh
go install dev.gaijin.team/go/exhaustruct/v5/cmd/exhaustruct@latest
```

```sh
exhaustruct ./...
```

## 身份与边界

- 身份：Gaijin Entertainment 组织仓库；个人创建者及具体维护者待验证。
- 限制：可能与有意省略零值字段的风格冲突；v5 路径不可与旧主版本混用。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
