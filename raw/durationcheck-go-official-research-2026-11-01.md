# github.com/charithe/durationcheck 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/charithe/durationcheck`；官方模块：`github.com/charithe/durationcheck`。
- 用途：检查两个 time.Duration 相乘的可疑写法。
- [项目官方仓库](https://github.com/charithe/durationcheck)；[所查官方文档](https://github.com/charithe/durationcheck)；[Go Packages](https://pkg.go.dev/github.com/charithe/durationcheck)。
- [账号或组织主页](https://github.com/charithe)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/charithe/durationcheck/cmd/durationcheck
```

```text
durationcheck ./...
```

## 边界

- 规则针对可疑乘法，不能覆盖所有时间单位错误。
- 版本由目标项目锁定；示例未在本机下载或编译。
