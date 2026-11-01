# github.com/knadh/koanf/providers/file 官方资料查阅记录

> 2026-11-01 查阅。本文是对官方页面的研究笔记，并非官方原文副本；收件箱原文未改，示例未在本机运行。

## 模块与版本

- 收件箱条目和模块路径均为 `github.com/knadh/koanf/providers/file`。
- [Go Packages 包文档](https://pkg.go.dev/github.com/knadh/koanf/providers/file) 检索结果显示 v1.2.1（2025-12-19 发布）；页面同时提示该包页面并非模块最新版本，目标项目应以 `go.mod` 锁定版本核对。
- [项目 README 的安装与 file provider 示例](https://github.com/knadh/koanf/blob/master/README.md)；[当前分支模块 go.mod](https://github.com/knadh/koanf/blob/master/providers/file/go.mod) 声明 Go 1.23.0、fsnotify v1.9.0。当前分支与 v1.2.1 不能视为同一版本快照。

## API 与用法

- [Go Packages 文档](https://pkg.go.dev/github.com/knadh/koanf/providers/file)：`file.Provider(path)` 返回 provider；`ReadBytes()` 读磁盘文件原始字节；`Read()` 不支持；`Watch(cb)` 监视变化，`Unwatch()` 停止。
- [官方 README：Reading from files](https://github.com/knadh/koanf/blob/master/README.md)：文件 provider 与 `json.Parser()` 等 parser 一起传给 koanf `Load`。文件内容格式由 parser 决定。
- [当前分支 file.go](https://github.com/knadh/koanf/blob/master/providers/file/file.go)：`ReadBytes()` 使用 `os.ReadFile`；监听通过 fsnotify 监视父目录，支持符号链接变化；同一 provider 重复启动监听返回错误。
- [官方 README：Watching file for changes](https://github.com/knadh/koanf/blob/master/README.md)：回调可重新加载配置；与并发读取同一 koanf 对象时需自行加锁。README 仍写 file provider 的 `event` 总为 nil；当前分支源码在变更回调中传入事件。具体行为须按选定版本核对。

## 作者与关联

- [koanf LICENSE](https://github.com/knadh/koanf/blob/master/LICENSE) 署名 2019 Kailash Nadh；[其 GitHub 主页](https://github.com/knadh) 确认账号身份；[koanf Releases](https://github.com/knadh/koanf/releases) 显示该账号发布项目版本。证据支持项目原始署名及维护参与，不能推出 file 子模块的唯一创建者或完整当前维护者名单。
- 同账号项目 [goyesql](https://github.com/knadh/goyesql)、[stuffbin](https://github.com/knadh/stuffbin) 已在此前作者资料中核实，尚未摄入。

## 待验证

- 用户项目使用的 provider、koanf 核心和 parser 版本及 Go 版本；file 子模块具体创建者与当前维护者；示例在目标环境的运行表现。
