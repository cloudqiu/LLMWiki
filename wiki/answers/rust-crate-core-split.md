---
title: "为什么 Rust 项目常拆出 -core crate？以 time 为例"
type: answer
created: 2026-11-02
updated: 2026-11-02
tags: [rust, cargo, library-design]
status: growing
sources: [raw/rust-core-crate-split-official-research-2026-11-02.md, raw/time-rust-official-research-2026-11-01.md, raw/time-core-rust-official-research-2026-11-01.md]
---

# 为什么 Rust 项目常拆出 -core crate？

> 归档自 2026-11-02 的查询。例子：[[time-rust]] 与 [[time-core-rust]]。

## 回答

`foo-core` 是**项目的命名习惯**：把多个 crate 要共用的基础类型、算法或内部接口放到较小的 package，`foo` 再向使用者提供主要 API。它不是 Cargo 强制的结构，也不是 Rust 标准库 `core` 的别名。

常见动机包括共享实现、控制依赖边界、让可选功能留在独立 crate，以及给过程宏提供可共用的基础代码。具体动机必须看该项目的依赖图；名称本身不能证明 `no_std`、体积或 API 稳定性。Cargo 的 workspace 方便一起管理这些 package，但 workspace 不会自动决定谁是公共入口。

`time` 的依赖关系可概括为：

```text
应用 ──> time ─────────> time-core
          └─ macros feature ─> time-macros ─> time-core
```

`time-macros` 是独立的 `proc-macro` crate；Rust 要求过程宏定义在这类 crate 中。`time` 的 `macros` feature 可选地启用它，而 `time-core` 是 `time` 的普通依赖。`time-core` 文档明确说它属于实现细节，不建议直接依赖。通常应用应依赖 `time`，需要宏时启用其 `macros` feature。

## 依据

- `raw/rust-core-crate-split-official-research-2026-11-02.md`「官方依据」记录 Cargo、Rust Reference、time 仓库配置与 time-core 文档。
- [[time-rust]]、[[time-core-rust]]；`raw/time-rust-official-research-2026-11-01.md` 与 `raw/time-core-rust-official-research-2026-11-01.md`「用途」。

## 后续

- 比较别的 `-core` crate 时，分别核查其 Cargo.toml、公开文档及是否推荐直接依赖；不要仅凭后缀类推。
