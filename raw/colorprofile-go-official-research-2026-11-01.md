# github.com/charmbracelet/colorprofile 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/charmbracelet/colorprofile`；官方模块：`github.com/charmbracelet/colorprofile`。
- 用途：检测终端色彩能力并自动降级颜色输出。
- [项目官方仓库](https://github.com/charmbracelet/colorprofile)；[所查官方文档](https://github.com/charmbracelet/colorprofile)；[Go Packages](https://pkg.go.dev/github.com/charmbracelet/colorprofile)。
- [账号或组织主页](https://github.com/charmbracelet)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/charmbracelet/colorprofile
```

```go
profile := colorprofile.Detect(os.Stdout, os.Environ()); _ = profile
```

## 边界

- 检测结果受输出目标和环境变量影响。
- 版本由目标项目锁定；示例未在本机下载或编译。
