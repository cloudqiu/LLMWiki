# github.com/ccojocar/zxcvbn-go 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/ccojocar/zxcvbn-go`；官方模块：`github.com/ccojocar/zxcvbn-go`。
- 用途：估计密码强度并识别常见词和模式。
- [项目官方仓库](https://github.com/ccojocar/zxcvbn-go)；[所查官方文档](https://github.com/ccojocar/zxcvbn-go)；[Go Packages](https://pkg.go.dev/github.com/ccojocar/zxcvbn-go)。
- [账号或组织主页](https://github.com/ccojocar)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/ccojocar/zxcvbn-go
```

```go
strength := zxcvbn.PasswordStrength("example-password", []string{"username"}); _ = strength
```

## 边界

- 这是已归档 nbutton23 版本的活跃 fork；评分是估计，不是密码安全保证。
- 版本由目标项目锁定；示例未在本机下载或编译。
