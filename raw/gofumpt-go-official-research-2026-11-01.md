# mvdan.cc/gofumpt 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`mvdan.cc/gofumpt`。
- 官方模块：`mvdan.cc/gofumpt`。
- 用途：在 gofmt 基础上施加更严格的 Go 代码格式规则。
- [官方项目或文档](https://github.com/mvdan/gofumpt)；[Go Packages](https://pkg.go.dev/mvdan.cc/gofumpt)。

## 安装与典型用法

```sh
go install mvdan.cc/gofumpt@latest
```

```sh
gofumpt -w main.go
```

## 身份与边界

- 身份：mvdan 项目账号发布；个人创建者与当前维护者待验证。
- 限制：-w 原地修改文件；团队应统一工具版本。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
