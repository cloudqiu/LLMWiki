# github.com/bits-and-blooms/bitset 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/bits-and-blooms/bitset`。
- 核对模块：`github.com/bits-and-blooms/bitset`。
- [项目官方资料](https://pkg.go.dev/github.com/bits-and-blooms/bitset)；[Go Packages](https://pkg.go.dev/github.com/bits-and-blooms/bitset)。
- 用途：用可扩展位集合存储非负整数的布尔状态。

## 安装与用法

```sh
go get github.com/bits-and-blooms/bitset
```

```go
b := bitset.New(128).Set(10); ok := b.Test(10); _ = ok
```

## 身份与限制

- 仓库账号 bits-and-blooms；个人创建者和当前维护者待验证。
- 容量随最大设置位增长，清除位不会自动缩小内存。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。
