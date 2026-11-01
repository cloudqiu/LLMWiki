---
title: "github.com/clipperhouse/uax29/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/uax29-v2-go-official-research-2026-11-01.md]
---

# github.com/clipperhouse/uax29/v2

## 用途与适用场景

按 Unicode UAX #29 分割字素、单词和句子。（[[uax29-v2-go-official-research]]）

## 依赖与版本

- 模块：`github.com/clipperhouse/uax29/v2`；安装或依赖声明：`go get github.com/clipperhouse/uax29/v2/words`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[matt-sherman]]：官方主页证实 Matt Sherman 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```go
words := words.FromString("Hello, 世界!"); for words.Next() { fmt.Println(words.Value()) }
```

## 关键限制

- 使用 v2 子包 import；分词边界按 Unicode 标准，不等于应用语义词。

## 来源

- [[uax29-v2-go-official-research]]；[官方仓库](https://github.com/clipperhouse/uax29)；[官方文档](https://github.com/clipperhouse/uax29)。
- 本地查阅记录：`raw/uax29-v2-go-official-research-2026-11-01.md`。
