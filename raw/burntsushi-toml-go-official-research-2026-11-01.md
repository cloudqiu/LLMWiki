# github.com/BurntSushi/toml 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/BurntSushi/toml`。
- 核对模块：`github.com/BurntSushi/toml`。
- [项目官方资料](https://github.com/BurntSushi/toml)；[Go Packages](https://pkg.go.dev/github.com/BurntSushi/toml)。
- 用途：把 TOML 文本解码到 Go 结构体并编码回 TOML。

## 安装与用法

```sh
go get github.com/BurntSushi/toml@latest
```

```go
var cfg struct{ Age int }; _, err := toml.Decode("Age = 25", &cfg); _ = err
```

## 身份与限制

- [[andrew-gallant]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。
- 解码只处理导出字段；官方 README 要求 Go 1.19 或更新。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。

## 身份与其他项目证据

- [官方个人或组织主页](https://github.com/BurntSushi)核对账号身份。
- [同账号或组织的其他项目](https://github.com/BurntSushi/ripgrep)；仅作待摄入线索，个人创建者/维护者角色待验证。
