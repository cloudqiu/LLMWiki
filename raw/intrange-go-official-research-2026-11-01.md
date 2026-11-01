# github.com/ckaznocha/intrange 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/ckaznocha/intrange`；官方模块：`github.com/ckaznocha/intrange`。
- 用途：找出可改用 Go 1.22 整数 range 的循环。
- [项目官方仓库](https://github.com/ckaznocha/intrange)；[所查官方文档](https://github.com/ckaznocha/intrange)；[Go Packages](https://pkg.go.dev/github.com/ckaznocha/intrange)。
- [账号或组织主页](https://github.com/ckaznocha)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/ckaznocha/intrange
```

```text
通过 golangci-lint 启用 intrange 检查项目
```

## 边界

- 目标项目的 Go 版本须至少 1.22；独立 CLI 用法待验证。
- 版本由目标项目锁定；示例未在本机下载或编译。
