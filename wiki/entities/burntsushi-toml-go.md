---
title: "github.com/BurntSushi/toml"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/burntsushi-toml-go-official-research-2026-11-01.md]
---

# github.com/BurntSushi/toml

## 用途与适用场景

把 TOML 文本解码到 Go 结构体并编码回 TOML。（[[burntsushi-toml-go-official-research]]）

## 依赖与版本

- 模块：`github.com/BurntSushi/toml`；安装或依赖声明：`go get github.com/BurntSushi/toml@latest`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- [[andrew-gallant]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```go
var cfg struct{ Age int }; _, err := toml.Decode("Age = 25", &cfg); _ = err
```

## 关键限制

- 解码只处理导出字段；官方 README 要求 Go 1.19 或更新。

## 来源

- [[burntsushi-toml-go-official-research]]；[官方资料](https://github.com/BurntSushi/toml)；[Go Packages](https://pkg.go.dev/github.com/BurntSushi/toml)。
- 本地研究笔记：`raw/burntsushi-toml-go-official-research-2026-11-01.md`。
