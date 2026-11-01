# github.com/xiang90/probing 官方资料查阅记录

> 2026-11-01 查阅；这是 Codex 的研究笔记，不是官方原文副本。示例未在目标环境运行。

## 模块与来源

- 收件箱与官方模块路径：`github.com/xiang90/probing`。
- [Go Packages 模块](https://pkg.go.dev/github.com/xiang90/probing)；[示例子包/API](https://pkg.go.dev/github.com/xiang90/probing)；[官方项目仓库](https://github.com/xiang90/probing)。查阅日期：2026-11-01；具体版本以目标项目 `go.mod` 为准。
- 用途：通过 HTTP 健康端点持续探测目标，统计丢包和往返时间。

## 典型 API

示例是按官方包文档或项目 README 摘出的最小片段；如需运行，要补齐 import、外部对象和运行条件。

```go
p := probing.NewProber(http.DefaultTransport)
err := p.AddHTTP("peer", 5*time.Second, []string{"http://localhost:12345/health"})
if err != nil { panic(err) }
```

## 创建者、维护者和关联

- xiang90 仓库归属可核实；个人创建者及当前维护者待验证。
- 角色证据：[官方项目仓库](https://github.com/xiang90/probing)。仓库、版权、账号、发布者分别说明不同角色；不从其中一项推断完整维护者名单。

## 关键边界与待验证

- 官方 README 的旧片段与 Go Packages 当前 AddHTTP 签名有差异；按目标版本核对。部署前还需设置对应 HTTP handler。
- 目标项目版本、完整依赖及示例运行表现待验证。
