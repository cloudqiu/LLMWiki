# github.com/breml/errchkjson 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/breml/errchkjson`；官方模块：`github.com/breml/errchkjson`。
- 用途：检查 JSON 编码的不可支持类型与可省略的错误处理。
- [项目官方仓库](https://github.com/breml/errchkjson)；[所查官方文档](https://github.com/breml/errchkjson)；[Go Packages](https://pkg.go.dev/github.com/breml/errchkjson)。
- [账号或组织主页](https://github.com/breml)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go install github.com/breml/errchkjson/cmd/errchkjson@latest
```

```text
errchkjson ./...
```

## 边界

- 类型检查有适用边界；忽略编码错误前须确认类型不会演变。
- 版本由目标项目锁定；示例未在本机下载或编译。
