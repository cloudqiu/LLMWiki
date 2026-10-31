# github.com/knadh/koanf/providers/rawbytes 官方资料查阅记录

> 2026-10-31 查阅。本文是 Codex 对官方页面的研究笔记，并非官方原文副本。收件箱原文保留不动；API 示例未在本机运行。

## 1. 模块与用途

- 收件箱条目：`github.com/knadh/koanf/providers/rawybytes`（原文有拼写错误，见第 4 节）。
- 官方模块 / import：`github.com/knadh/koanf/providers/rawbytes`；示例导入 `github.com/knadh/koanf/providers/rawbytes`。
- 用途：把内存中的 []byte 作为 koanf 配置源；常与 JSON、TOML 等 parser 配合。
- Go Packages：[模块页面](https://pkg.go.dev/github.com/knadh/koanf/providers/rawbytes)；[示例包页面](https://pkg.go.dev/github.com/knadh/koanf/providers/rawbytes)。查阅日期：2026-10-31。具体版本以项目 go.mod 锁定；本地未下载依赖，未核对用户项目版本。

## 2. 典型 API

官方包文档显示如下调用方式；示例为教学片段，所需 import 和外部对象需按项目补齐，未运行：

```go
k := koanf.New(".")
err := k.Load(rawbytes.Provider([]byte(`{"port":8080}`)), json.Parser())
fmt.Println(k.Int("port"), err)
```

## 3. 作者与关联项目

- 官方仓库：https://github.com/knadh/koanf。
- 角色判断：[[kailash-nadh]]：koanf 项目原始署名；子模块的独立作者待验证。
- 同一账号或组织的其他可查项目：[goyesql](https://github.com/knadh/goyesql)、[stuffbin](https://github.com/knadh/stuffbin)。仓库归属不自动证明个人独立创作，清单也不代表全部作品。

## 4. 选用边界与待验证

- 只提供原始字节，不负责解析格式；需要另配 parser。收件箱写作 rawybytes，官方路径为 rawbytes。
- 需在目标 Go 版本、操作系统和用户项目中编译运行；本轮无法从本机直接获取模块。
- 收件箱原文 `github.com/knadh/koanf/providers/rawybytes`；官方模块为 `github.com/knadh/koanf/providers/rawbytes`。
