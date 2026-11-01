# github.com/breml/bidichk 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/breml/bidichk`；官方模块：`github.com/breml/bidichk`。
- 用途：检测源码中可能改变显示顺序的危险双向 Unicode 控制符。
- [项目官方仓库](https://github.com/breml/bidichk)；[所查官方文档](https://github.com/breml/bidichk)；[Go Packages](https://pkg.go.dev/github.com/breml/bidichk)。
- [账号或组织主页](https://github.com/breml)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go install github.com/breml/bidichk/cmd/bidichk@latest
```

```text
bidichk ./...
```

## 边界

- 仅检查配置定义的危险字符，不等于完整代码安全审计。
- 版本由目标项目锁定；示例未在本机下载或编译。
