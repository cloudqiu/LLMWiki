# github.com/ashanbrown/makezero/v2 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/ashanbrown/makezero/v2`。
- 核对模块：`github.com/ashanbrown/makezero/v2`。
- [项目官方资料](https://pkg.go.dev/github.com/ashanbrown/makezero/v2)；[Go Packages](https://pkg.go.dev/github.com/ashanbrown/makezero/v2)。
- 用途：检查先创建非零长度 slice 又 append 导致多出零值元素。

## 安装与用法

```sh
go install github.com/ashanbrown/makezero/v2@latest
```

```text
makezero ./...
```

## 身份与限制

- 仓库账号 ashanbrown；个人创建者和当前维护者待验证。
- 默认仅报告后续 append 的相关模式；-always 会扩大检查范围。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。
