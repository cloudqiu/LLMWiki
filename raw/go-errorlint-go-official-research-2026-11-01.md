# codeberg.org/polyfloyd/go-errorlint 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`codeberg.org/polyfloyd/go-errorlint`。
- 官方模块：`codeberg.org/polyfloyd/go-errorlint`。
- 用途：检查 Go 错误比较、类型断言与包装等用法，适合迁移至 errors.Is/As。
- [官方项目或文档](https://pkg.go.dev/codeberg.org/polyfloyd/go-errorlint)；[Go Packages](https://pkg.go.dev/codeberg.org/polyfloyd/go-errorlint)。

## 安装与典型用法

```sh
go install codeberg.org/polyfloyd/go-errorlint@latest
```

```sh
go-errorlint ./...
```

## 身份与边界

- 身份：Codeberg 账号 polyfloyd；个人身份与当前维护者待验证。
- 限制：旧 GitHub 仓库已归档并指向 Codeberg；-fix 选项可能改变代码，先审阅差异。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
