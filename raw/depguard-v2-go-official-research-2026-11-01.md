# github.com/OpenPeeDeeP/depguard/v2 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/OpenPeeDeeP/depguard/v2`。
- 核对模块：`github.com/OpenPeeDeeP/depguard/v2`。
- [项目官方资料](https://github.com/OpenPeeDeeP/depguard/blob/v2/README.md)；[Go Packages](https://pkg.go.dev/github.com/OpenPeeDeeP/depguard/v2)。
- 用途：按 allow/deny 规则检查 Go import。

## 安装与用法

```sh
go get github.com/OpenPeeDeeP/depguard/v2
```

```text
在 .depguard.yml 定义规则后运行 depguard ./...
```

## 身份与限制

- 仓库账号 OpenPeeDeeP；个人创建者和当前维护者待验证。
- 独立 CLI 的官方 README 安装命令仍指向无 /v2 的子路径，实际版本须核对；配置默认匹配规则需审阅。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。
