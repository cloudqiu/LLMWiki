# github.com/catenacyber/perfsprint 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/catenacyber/perfsprint`；官方模块：`github.com/catenacyber/perfsprint`。
- 用途：找出可用 strconv 等更直接操作替代的 fmt 格式化调用。
- [项目官方仓库](https://github.com/catenacyber/perfsprint)；[所查官方文档](https://github.com/catenacyber/perfsprint)；[Go Packages](https://pkg.go.dev/github.com/catenacyber/perfsprint)。
- [账号或组织主页](https://github.com/catenacyber)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go install github.com/catenacyber/perfsprint@latest
```

```text
perfsprint ./...
```

## 边界

- 部分重写改变 nil 错误等边界行为；--fix 前需审阅。
- 版本由目标项目锁定；示例未在本机下载或编译。
