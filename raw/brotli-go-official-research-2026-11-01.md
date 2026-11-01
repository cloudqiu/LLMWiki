# github.com/andybalholm/brotli 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/andybalholm/brotli`。
- 核对模块：`github.com/andybalholm/brotli`。
- [项目官方资料](https://pkg.go.dev/github.com/andybalholm/brotli)；[Go Packages](https://pkg.go.dev/github.com/andybalholm/brotli)。
- 用途：纯 Go Brotli 编码与解码，适合 HTTP 压缩或文件流。

## 安装与用法

```sh
go get github.com/andybalholm/brotli
```

```go
w := brotli.NewWriter(dst); _, err := w.Write(data); if err == nil { err = w.Close() }; _ = err
```

## 身份与限制

- 仓库账号 andybalholm；个人创建者和当前维护者待验证。
- Writer 可能缓冲输出；完成时必须 Close。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。
