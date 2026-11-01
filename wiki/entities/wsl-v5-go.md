---
title: "github.com/bombsimon/wsl/v5"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/wsl-v5-go-official-research-2026-11-01.md]
---

# github.com/bombsimon/wsl/v5

## 用途与适用场景

检查 Go 语句间的空行和分组风格。（[[wsl-v5-go-official-research]]）

## 依赖与版本

- 模块：`github.com/bombsimon/wsl/v5`；安装或依赖声明：`go install github.com/bombsimon/wsl/v5/cmd/wsl@latest`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[simon-sawert]]：官方主页证实 Simon Sawert 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```text
wsl ./...
```

## 关键限制

- 格式建议带主观性；v5 配置不能直接按旧版本推定；Windows 上 wsl 命令可能与系统 WSL 可执行文件同名，运行时须确认所调用的程序。

## 来源

- [[wsl-v5-go-official-research]]；[官方仓库](https://github.com/bombsimon/wsl)；[官方文档](https://github.com/bombsimon/wsl)。
- 本地查阅记录：`raw/wsl-v5-go-official-research-2026-11-01.md`。
