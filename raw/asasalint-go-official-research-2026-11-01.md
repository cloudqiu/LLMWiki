# github.com/alingse/asasalint 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/alingse/asasalint`。
- 核对模块：`github.com/alingse/asasalint`。
- [项目官方资料](https://github.com/alingse/asasalint)；[Go Packages](https://pkg.go.dev/github.com/alingse/asasalint)。
- 用途：找出把 any slice 错误地作为单个 any 传入可变参数函数的情况。

## 安装与用法

```sh
go install github.com/alingse/asasalint/cmd/asasalint@latest
```

```text
asasalint ./...
```

## 身份与限制

- 仓库账号 alingse；个人创建者和当前维护者待验证。
- 可用 -e 排除有意使用的函数；需结合项目代码判断。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。
