# github.com/MirrexOne/unqueryvet 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/MirrexOne/unqueryvet`。
- 核对模块：`github.com/MirrexOne/unqueryvet`。
- [项目官方资料](https://github.com/MirrexOne/unqueryvet)；[Go Packages](https://pkg.go.dev/github.com/MirrexOne/unqueryvet)。
- 用途：检查 SQL 查询中 SELECT * 等不显式选列的写法。

## 安装与用法

```sh
go install github.com/MirrexOne/unqueryvet/cmd/unqueryvet@latest
```

```text
unqueryvet ./...
```

## 身份与限制

- 仓库账号 MirrexOne；个人创建者和当前维护者待验证。
- 主要识别静态可分析的 SQL 字符串；动态拼接覆盖范围待验证。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。
