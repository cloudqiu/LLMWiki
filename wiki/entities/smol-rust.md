---
title: "smol"
type: entity
entity_type: tool
created: 2026-11-04
updated: 2026-11-04
tags: [rust, library, async, runtime]
status: growing
sources: [raw/smol-rust-official-research-2026-11-04.md]
---

# smol

## 用途与适用场景

小型 Rust 异步运行时，将执行器、网络、异步 I/O 与计时器等组件作为统一入口重新导出。适合需要直接启动异步任务、使用其 I/O API 的应用；与 [[async-executor-rust]] 等组件关系见 [[rust-async-runtime-boundaries]]。（[[smol-rust-official-research]]）

## 依赖与版本

- 语言 / 生态：Rust / Cargo。
- 查阅版本 / 日期：docs.rs 2.0.2，2026-11-04；实际版本以项目 Cargo.lock 为准。
- 依赖声明：`smol = "2"`。查阅时仓库 manifest 的 `rust-version` 为 1.85；目标项目应按所锁定版本核对。

## 作者与维护者

- manifest 署名作者：[[stjepan-glavina|Stjepan Glavina]]，依据官方 `Cargo.toml` 的 `authors` 字段。
- 创建者：待验证；manifest 署名不能单独证明创建过程。
- 当前维护者：待验证；smol-rs 托管与提交活动不能单独证明具体维护职责。

## 典型用法

以下片段基于 2.0.2 公开的 `block_on` 与 `spawn` API 整理，**未在本机编译运行**。

1. 在普通 `main` 中驱动一个 future：

```rust
fn main() {
    let value = smol::block_on(async { 1 + 2 });
    assert_eq!(value, 3);
}
```

2. 在运行时中启动并等待任务：

```rust
fn main() {
    smol::block_on(async {
        let task = smol::spawn(async { 1 + 2 });
        assert_eq!(task.await, 3);
    });
}
```

## 关键限制

- 全局 `spawn` 执行器默认单线程；需要其他调度方式时查看 `Executor` 或项目指向的 `smol-macros`。
- Tokio 库的 future 或 I/O 类型接入 smol 时需检查 `async-compat` 适配；标准 `Future` 接口本身不保证底层运行时服务兼容。
- [[async-std-rust|async-std]] 的项目文档建议转向 smol，但迁移时仍须核对各 API，不应假设直接替换。

## 来源

- [[smol-rust-official-research]]；本地记录 `raw/smol-rust-official-research-2026-11-04.md`。
- [官方仓库](https://github.com/smol-rs/smol)、[官方文档（2.0.2）](https://docs.rs/smol/2.0.2/smol/)、[官方 manifest](https://github.com/smol-rs/smol/blob/master/Cargo.toml)。
