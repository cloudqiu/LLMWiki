# go.yaml.in/yaml/v2 官方资料查阅记录

> 2026-11-01 查阅；这是 Codex 的研究笔记，不是官方原文副本。示例未在目标环境运行。

## 模块与来源

- 收件箱与官方模块路径：`go.yaml.in/yaml/v2`。
- [Go Packages 模块](https://pkg.go.dev/go.yaml.in/yaml/v2)；[示例子包/API](https://pkg.go.dev/go.yaml.in/yaml/v2)；[官方项目仓库](https://github.com/go-yaml/yaml)。查阅日期：2026-11-01；具体版本以目标项目 `go.mod` 为准。
- 用途：将 YAML 编解码为 Go 值，提供严格解码以发现未知字段和重复键。

## 典型 API

示例是按官方包文档或项目 README 摘出的最小片段；如需运行，要补齐 import、外部对象和运行条件。

```go
var cfg struct { Name string `yaml:"name"` }
err := yaml.UnmarshalStrict([]byte("name: demo\n"), &cfg)
if err != nil { panic(err) }
```

## 创建者、维护者和关联

- 官方 README 由 Gustavo Niemeyer 自述为早期项目并声明停止维护。
- 角色证据：[官方项目仓库](https://github.com/go-yaml/yaml)。仓库、版权、账号、发布者分别说明不同角色；不从其中一项推断完整维护者名单。

## 关键边界与待验证

- 官方项目明确标为 unmaintained，仓库已归档；当前路径是 go.yaml.in/yaml/v2，旧 gopkg.in 路径须另行核对。
- 目标项目版本、完整依赖及示例运行表现待验证。
