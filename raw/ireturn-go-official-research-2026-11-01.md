# github.com/butuzov/ireturn 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/butuzov/ireturn`；官方模块：`github.com/butuzov/ireturn`。
- 用途：提示函数返回接口类型的设计选择。
- [项目官方仓库](https://github.com/butuzov/ireturn)；[所查官方文档](https://github.com/butuzov/ireturn)；[Go Packages](https://pkg.go.dev/github.com/butuzov/ireturn)。
- [账号或组织主页](https://github.com/butuzov)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/butuzov/ireturn
```

```text
通过 golangci-lint 启用 ireturn 检查项目
```

## 边界

- 返回接口并非一概错误；框架接口和 API 边界需按需排除。
- 版本由目标项目锁定；示例未在本机下载或编译。
