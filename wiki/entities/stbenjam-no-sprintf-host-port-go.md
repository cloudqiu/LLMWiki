---
title: "github.com/stbenjam/no-sprintf-host-port"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/stbenjam-no-sprintf-host-port-go-official-research-2026-11-01.md]
---

# github.com/stbenjam/no-sprintf-host-port

## 用途与适用场景

检测以 Sprintf 拼接 host:port 的写法。（[[stbenjam-no-sprintf-host-port-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/stbenjam/no-sprintf-host-port`；项目中执行 `go get github.com/stbenjam/no-sprintf-host-port`。
- 2026-11-01 查阅官方资料；实际版本由目标项目锁定。

## 作者与维护者

- 作者待验证；仓库所属账号不单独证明个人创建者。
- 当前维护者：待验证。

## 典型用法

以下最小片段对照官方资料整理，**未在本机运行**。Go 片段需补齐 import、变量与外围函数；命令需在相应项目中执行。

```sh
golangci-lint run --enable-only nosprintfhostport ./...
```

## 关键限制

- 应使用 net.JoinHostPort 处理 IPv6 地址。

## 来源

- [[stbenjam-no-sprintf-host-port-go-official-research]]；[官方仓库](https://github.com/stbenjam/no-sprintf-host-port)；[README 或版本文档](https://raw.githubusercontent.com/stbenjam/no-sprintf-host-port/main/README.md)。
- 本地笔记：`raw/stbenjam-no-sprintf-host-port-go-official-research-2026-11-01.md`。
