# github.com/bep/golibsass 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/bep/golibsass`。
- 核对模块：`github.com/bep/golibsass`。
- [项目官方资料](https://github.com/bep/golibsass)；[Go Packages](https://pkg.go.dev/github.com/bep/golibsass)。
- 用途：从 Go 调用 LibSass 编译 SCSS。

## 安装与用法

```sh
go get github.com/bep/golibsass
```

```go
t, err := libsass.New(libsass.Options{OutputStyle: libsass.CompressedStyle}); _ = t; _ = err
```

## 身份与限制

- [[bjorn-erik-pedersen]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。
- 绑定 LibSass 原生实现；与 Dart Sass 路线和运行要求不同。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。
