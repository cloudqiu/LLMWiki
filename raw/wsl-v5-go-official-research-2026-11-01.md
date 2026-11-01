# github.com/bombsimon/wsl/v5 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/bombsimon/wsl/v5`；官方模块：`github.com/bombsimon/wsl/v5`。
- 用途：检查 Go 语句间的空行和分组风格。
- [项目官方仓库](https://github.com/bombsimon/wsl)；[所查官方文档](https://github.com/bombsimon/wsl)；[Go Packages](https://pkg.go.dev/github.com/bombsimon/wsl/v5)。
- [账号或组织主页](https://github.com/bombsimon)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go install github.com/bombsimon/wsl/v5/cmd/wsl@latest
```

```text
wsl ./...
```

## 边界

- 格式建议带主观性；v5 配置不能直接按旧版本推定；Windows 上 wsl 命令可能与系统 WSL 可执行文件同名，运行时须确认所调用的程序。
- 版本由目标项目锁定；示例未在本机下载或编译。
