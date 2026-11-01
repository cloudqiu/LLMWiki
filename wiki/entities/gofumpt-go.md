---
title: "mvdan.cc/gofumpt"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/gofumpt-go-official-research-2026-11-01.md]
---

# mvdan.cc/gofumpt

## 用途与适用场景

在 gofmt 基础上施加更严格的 Go 代码格式规则。（[[gofumpt-go-official-research]]）

## 依赖与版本

- 官方模块：`mvdan.cc/gofumpt`。
- 安装或依赖声明：`go install mvdan.cc/gofumpt@latest`。
- 查阅日期：2026-11-01；具体版本以目标项目锁定为准。

## 作者与维护者

- mvdan 项目账号发布；个人创建者与当前维护者待验证。

## 典型用法

下面示例以官方文档或项目 README 为依据；**未在本机运行**。命令需在适当 Go 项目中执行；Go 代码片段需补齐 import 与外围函数。

```sh
gofumpt -w main.go
```

## 关键限制

- -w 原地修改文件；团队应统一工具版本。

## 来源

- [[gofumpt-go-official-research]]；[官方项目或文档](https://github.com/mvdan/gofumpt)；[Go Packages](https://pkg.go.dev/mvdan.cc/gofumpt)。
- 本地原始资料：`raw/gofumpt-go-official-research-2026-11-01.md`。
