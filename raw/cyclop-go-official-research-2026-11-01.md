# github.com/bkielbasa/cyclop 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/bkielbasa/cyclop`；官方模块：`github.com/bkielbasa/cyclop`。
- 用途：检测 Go 函数和包的圈复杂度。
- [项目官方仓库](https://github.com/bkielbasa/cyclop)；[所查官方文档](https://github.com/bkielbasa/cyclop)；[Go Packages](https://pkg.go.dev/github.com/bkielbasa/cyclop)。
- [账号或组织主页](https://github.com/bkielbasa)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/bkielbasa/cyclop/cmd/cyclop
```

```text
cyclop .
```

## 边界

- 官方 README 使用 cmd/cyclop 安装；复杂度阈值需按项目配置。
- 版本由目标项目锁定；示例未在本机下载或编译。
