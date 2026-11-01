# github.com/santhosh-tekuri/jsonschema/v6 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 中文研究笔记，不是官方原文副本；示例未在本机运行。

## 路径与来源

- 收件箱原条目：`github.com/santhosh-tekuri/jsonschema/v6`；核实后的路径：`github.com/santhosh-tekuri/jsonschema/v6`。
- [官方仓库](https://github.com/santhosh-tekuri/jsonschema)；[所查 README 或版本文档](https://pkg.go.dev/github.com/santhosh-tekuri/jsonschema/v6)；[Go Packages 入口](https://pkg.go.dev/github.com/santhosh-tekuri/jsonschema/v6)。
- 在 Go 项目中声明依赖：`go get github.com/santhosh-tekuri/jsonschema/v6`。
- 仓库账号可确认项目关联；具体个人创建者与现任维护者待验证。

## 用途与典型用法

- 编译和验证 JSON Schema。

```go
compiler := jsonschema.NewCompiler(); schema, err := compiler.Compile("schema.json"); _, _ = schema, err
```

## 边界与待验证

- v6 与 v5 API 需区分；示例文件路径需按实际 loader 设置。
- 示例未在本机编译或运行；按目标项目版本复核参数与 API。
