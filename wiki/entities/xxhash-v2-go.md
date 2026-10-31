---
title: "github.com/cespare/xxhash/v2"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/xxhash-v2-go-official-research-2026-10-31.md]
---

# github.com/cespare/xxhash/v2

## 用途与适用场景

计算快速的 XXH64 非密码学哈希。（[[xxhash-v2-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/cespare/xxhash/v2`；示例使用 `github.com/cespare/xxhash/v2`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 作者索引：[[caleb-spare]]。
- 仓库账号 cespare；个人姓名及完整维护角色待验证。
- 其他相关项目：[xxhash v1](https://github.com/cespare/xxhash)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
sum := xxhash.Sum64String("hello")
fmt.Println(sum)
```

## 关键限制

- 不能用于密码、签名或抗攻击散列；v2 import 路径必须带 /v2。

## 来源

- [[xxhash-v2-go-official-research]]
- [官方仓库](https://github.com/cespare/xxhash)；[Go Packages](https://pkg.go.dev/github.com/cespare/xxhash/v2)；[示例 API](https://pkg.go.dev/github.com/cespare/xxhash/v2)。
- 本地查阅记录：`raw/xxhash-v2-go-official-research-2026-10-31.md`。
