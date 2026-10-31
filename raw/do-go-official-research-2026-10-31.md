# github.com/samber/do 官方资料查阅记录

> 2026-10-31 查阅。本文是 Codex 对官方页面的研究笔记，并非官方原文副本。收件箱原文保留不动；API 示例未在本机运行。

## 1. 模块与用途

- 收件箱条目：`github.com/samber/do`。
- 官方模块 / import：`github.com/samber/do`；示例导入 `github.com/samber/do`。
- 用途：使用泛型注册、解析服务及管理依赖注入生命周期。
- Go Packages：[模块页面](https://pkg.go.dev/github.com/samber/do)；[示例包页面](https://pkg.go.dev/github.com/samber/do)。查阅日期：2026-10-31。具体版本以项目 go.mod 锁定；本地未下载依赖，未核对用户项目版本。

## 2. 典型 API

官方包文档显示如下调用方式；示例为教学片段，所需 import 和外部对象需按项目补齐，未运行：

```go
injector := do.New()
do.Provide(injector, func(*do.Injector) (int, error) { return 42, nil })
n, err := do.Invoke[int](injector)
fmt.Println(n, err)
```

## 3. 作者与关联项目

- 官方仓库：https://github.com/samber/do。
- 角色判断：[[samuel-berthe]]：GitHub 自述将 do 列为其 Go 库。
- 同一账号或组织的其他可查项目：[lo](https://github.com/samber/lo)、[mo](https://github.com/samber/mo)、[oops](https://github.com/samber/oops)。仓库归属不自动证明个人独立创作，清单也不代表全部作品。

## 4. 选用边界与待验证

- 这是 v1 模块；v2 使用 github.com/samber/do/v2，迁移时核对 API。
- 需在目标 Go 版本、操作系统和用户项目中编译运行；本轮无法从本机直接获取模块。

## 5. 账号身份核对

- [GitHub 个人主页](https://github.com/samber) 公开显示姓名 Samuel Berthe。仓库归属证明账号关联，不单独证明其为唯一作者或当前唯一维护者。
