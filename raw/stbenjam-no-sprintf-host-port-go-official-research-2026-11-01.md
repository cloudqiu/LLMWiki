# github.com/stbenjam/no-sprintf-host-port 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 中文研究笔记，不是官方原文副本；示例未在本机运行。

## 路径与来源

- 收件箱原条目：`github.com/stbenjam/no-sprintf-host-port`；核实后的路径：`github.com/stbenjam/no-sprintf-host-port`。
- [官方仓库](https://github.com/stbenjam/no-sprintf-host-port)；[所查 README 或版本文档](https://raw.githubusercontent.com/stbenjam/no-sprintf-host-port/main/README.md)；[Go Packages 入口](https://pkg.go.dev/github.com/stbenjam/no-sprintf-host-port)。
- 在 Go 项目中声明依赖：`go get github.com/stbenjam/no-sprintf-host-port`。
- 仓库账号可确认项目关联；具体个人创建者与现任维护者待验证。

## 用途与典型用法

- 检测以 Sprintf 拼接 host:port 的写法。

```sh
golangci-lint run --enable-only nosprintfhostport ./...
```

## 边界与待验证

- 应使用 net.JoinHostPort 处理 IPv6 地址。
- 示例未在本机编译或运行；按目标项目版本复核参数与 API。
