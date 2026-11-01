---
title: "github.com/leonklingele/grouper"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/leonklingele-grouper-go-official-research-2026-11-01.md]
---

# github.com/leonklingele/grouper

## 用途与适用场景

检查 import、const、var 声明分组。（[[leonklingele-grouper-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/leonklingele/grouper`；项目中执行 `go get github.com/leonklingele/grouper`。
- 查阅日期：2026-11-01；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不能单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段依据官方仓库或包资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数。

```sh
grouper -import-require-single-import -import-require-grouping ./...
```

## 关键限制

- 组别规则由标志决定。

## 来源

- [[leonklingele-grouper-go-official-research]]；[官方仓库](https://github.com/leonklingele/grouper)；[所查 README 或仓库说明](https://raw.githubusercontent.com/leonklingele/grouper/master/README.md)。
- 本地笔记：`raw/leonklingele-grouper-go-official-research-2026-11-01.md`。
