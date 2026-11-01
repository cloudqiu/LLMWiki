# github.com/bep/godartsass/v2 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/bep/godartsass/v2`。
- 核对模块：`github.com/bep/godartsass/v2`。
- [项目官方资料](https://pkg.go.dev/github.com/bep/godartsass/v2)；[Go Packages](https://pkg.go.dev/github.com/bep/godartsass/v2)。
- 用途：通过 Dart Sass Embedded 协议从 Go 编译 Sass/SCSS。

## 安装与用法

```sh
go get github.com/bep/godartsass/v2
```

```go
t, err := godartsass.Start(godartsass.Options{}); _ = t; _ = err
```

## 身份与限制

- [[bjorn-erik-pedersen]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。
- 需可用的 sass --embedded 可执行文件；v2 对应 Embedded 协议 v2。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。

## 身份与其他项目证据

- [官方个人或组织主页](https://github.com/bep)核对账号身份。
