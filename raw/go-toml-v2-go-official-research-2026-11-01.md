# github.com/pelletier/go-toml/v2 官方资料查阅记录

> 2026-11-01 查阅；这是 Codex 的研究笔记，不是官方原文副本。示例未在目标环境运行。

## 模块与来源

- 收件箱原文 `github.com/pelleiter/go-toml/v2`；官方模块 `github.com/pelletier/go-toml/v2`。
- [Go Packages 模块](https://pkg.go.dev/github.com/pelletier/go-toml/v2)；[示例子包/API](https://pkg.go.dev/github.com/pelletier/go-toml/v2)；[官方项目仓库](https://github.com/pelletier/go-toml)。查阅日期：2026-11-01；具体版本以目标项目 `go.mod` 为准。
- 用途：把 TOML 文本解码为 Go 结构，也可将结构编码为 TOML。

## 典型 API

示例是按官方包文档或项目 README 摘出的最小片段；如需运行，要补齐 import、外部对象和运行条件。

```go
var cfg struct { Name string `toml:"name"` }
err := toml.Unmarshal([]byte("name = \"demo\""), &cfg)
if err != nil { panic(err) }
fmt.Println(cfg.Name)
```

## 创建者、维护者和关联

- Thomas Pelletier 的官方 GitHub 主页将 go-toml 列为项目；具体版本维护者名单待验证。
- 角色证据：[官方项目仓库](https://github.com/pelletier/go-toml)。仓库、版权、账号、发布者分别说明不同角色；不从其中一项推断完整维护者名单。

## 关键边界与待验证

- 收件箱 pelleiter 为拼写错误；官方模块路径为 pelletier。TOML v2 与 v1 是不同导入路径。
- 目标项目版本、完整依赖及示例运行表现待验证。
