# github.com/alecthomas/chroma/v2 官方资料查阅记录

> 2026-11-01 查阅；本文为 Codex 研究笔记，并非官方原文副本。原收件箱未修改；示例未在本机运行。

## 来源与路径

- 收件箱原条目：`github.com/alecthomas/chroma/v2`。
- 核对模块：`github.com/alecthomas/chroma/v2`。
- [项目官方资料](https://pkg.go.dev/github.com/alecthomas/chroma/v2)；[Go Packages](https://pkg.go.dev/github.com/alecthomas/chroma/v2)。
- 用途：以纯 Go lexer 和 formatter 给代码做语法高亮。

## 安装与用法

```sh
go get github.com/alecthomas/chroma/v2
```

```go
err := quick.Highlight(os.Stdout, "package main", "go", "html", "monokai"); _ = err
```

## 身份与限制

- [[alec-thomas]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。
- 找不到 lexer、formatter 或 style 时可能返回 nil；应有回退处理。
- 版本以目标项目锁定为准；未在本机下载、编译或运行。

## 身份与其他项目证据

- [官方个人或组织主页](https://github.com/alecthomas)核对账号身份。
- [同账号或组织的其他项目](https://github.com/alecthomas/kong)；仅作待摄入线索，个人创建者/维护者角色待验证。
