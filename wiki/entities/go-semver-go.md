---
title: "github.com/coreos/go-semver"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/go-semver-go-official-research-2026-10-31.md]
---

# github.com/coreos/go-semver

## 用途与适用场景

解析和比较 SemVer 版本号。（[[go-semver-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/coreos/go-semver`；示例使用 `github.com/coreos/go-semver/semver`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 项目组织索引：[[coreos]]。
- coreos 组织仓库；个人作者与当前维护角色待验证。
- 其他相关项目：[go-systemd](https://github.com/coreos/go-systemd)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
v, err := semver.NewVersion("1.2.3")
fmt.Println(v, err)
```

## 关键限制

- 根仓库含命令；在 Go 代码中导入 /semver 子包。对前导 v、范围表达式的支持需按文档核对。

## 来源

- [[go-semver-go-official-research]]
- [官方仓库](https://github.com/coreos/go-semver)；[Go Packages](https://pkg.go.dev/github.com/coreos/go-semver)；[示例 API](https://pkg.go.dev/github.com/coreos/go-semver/semver)。
- 本地查阅记录：`raw/go-semver-go-official-research-2026-10-31.md`。
