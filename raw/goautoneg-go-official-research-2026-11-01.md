# github.com/munnerz/goautoneg 官方资料查阅记录

> 2026-11-01 查阅；这是 Codex 的研究笔记，不是官方原文副本。示例未在目标环境运行。

## 模块与来源

- 收件箱与官方模块路径：`github.com/munnerz/goautoneg`。
- [Go Packages 模块](https://pkg.go.dev/github.com/munnerz/goautoneg)；[示例子包/API](https://pkg.go.dev/github.com/munnerz/goautoneg)；[官方项目仓库](https://github.com/munnerz/goautoneg)。查阅日期：2026-11-01；具体版本以目标项目 `go.mod` 为准。
- 用途：根据 HTTP Accept 请求头从候选媒体类型中选择响应 Content-Type。

## 典型 API

示例是按官方包文档或项目 README 摘出的最小片段；如需运行，要补齐 import、外部对象和运行条件。

```go
choice := goautoneg.Negotiate("application/json, text/plain;q=0.5", []string{"text/plain", "application/json"})
fmt.Println(choice)
```

## 创建者、维护者和关联

- 镜像仓库 README 署名 Open Knowledge Foundation Ltd. 版权；个人创建者待验证。
- 角色证据：[官方项目仓库](https://github.com/munnerz/goautoneg)。仓库、版权、账号、发布者分别说明不同角色；不从其中一项推断完整维护者名单。

## 关键边界与待验证

- 仓库自称原 bitbucket.org/ww/goautoneg 的镜像；镜像账号不等于原创作者，原始创建者与现维护者待验证。
- 目标项目版本、完整依赖及示例运行表现待验证。
