---
title: "github.com/jackc/puddle/v2"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/puddle-v2-go-official-research-2026-10-31.md]
---

# github.com/jackc/puddle/v2

## 用途与适用场景

以泛型提供最小化的并发资源池。（[[puddle-v2-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/jackc/puddle/v2`；示例使用 `github.com/jackc/puddle/v2`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- [[jack-christensen]]：账号下的 pgx 家族资源池仓库；具体共同维护者待验证。
- 其他相关项目：[tern](https://github.com/jackc/tern)、[pglogrepl](https://github.com/jackc/pglogrepl)。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
pool, err := puddle.NewPool(&puddle.Config[int]{
    Constructor: func(context.Context) (int, error) { return 42, nil },
    Destructor: func(int) {}, MaxSize: 2,
})
if err != nil { log.Fatal(err) }
res, err := pool.Acquire(context.Background())
if err != nil { log.Fatal(err) }
fmt.Println(res.Value())
res.Release()
pool.Close()
```

## 关键限制

- Acquire 可阻塞，须传可取消 context；Release 后不得继续使用 Resource；Close 等待资源归还。

## 来源

- [[puddle-v2-go-official-research]]
- [官方仓库](https://github.com/jackc/puddle)；[Go Packages](https://pkg.go.dev/github.com/jackc/puddle/v2)；[示例 API](https://pkg.go.dev/github.com/jackc/puddle/v2)。
- 本地查阅记录：`raw/puddle-v2-go-official-research-2026-10-31.md`。
