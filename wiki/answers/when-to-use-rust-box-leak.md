---
title: "Rust 什么时候有意使用 Box::leak？"
type: answer
created: 2026-11-05
updated: 2026-11-05
tags: [rust, ownership, lifetimes, memory, box]
status: growing
sources:
  - raw/rust-box-leak-use-cases-official-research-2026-11-05.md
  - raw/rust-box-leak-string-chain-official-research-2026-11-05.md
---

# Rust 什么时候有意使用 `Box::leak`？

> 归档自 2026-11-05 的查询；`Box::leak(input.to_owned().into_boxed_str())` 的逐步类型变化见 [[rust-function-return-string-or-str]]。

## 回答

当数据**确实要在程序剩余时间一直有效**，而某接口只接受长期有效的引用、又没有合适的拥有者可供该接口借用时，才考虑 `Box::leak`。例如在启动阶段生成一个名称，交给要求 `&'static str` 且一直保留该引用的注册 API。这个注册 API 是说明设计条件的假设例子；是否需要泄漏须按真实 API 契约判断。标准库将 `Box::leak` 用于有意存活到程序剩余时间的数据。[`Box::leak` 文档](https://doc.rust-lang.org/std/boxed/struct.Box.html)。

这种做法较容易接受的条件是：初始化次数**有界**（通常一次）、对象不持有必须运行 `Drop` 才能正确结束的资源、直到进程结束都不需要回收。内存泄漏在 Rust 中可以是内存安全的，但仍会占用资源。[Rustonomicon：Leaking](https://doc.rust-lang.org/nomicon/leaking.html)。

## 先看是否有更合适的拥有者

若只是程序级单例，`OnceLock<String>` 可直接拥有运行时生成的值：

```rust
use std::sync::OnceLock;

static NAME: OnceLock<String> = OnceLock::new();

fn name() -> &'static str {
    NAME.get_or_init(|| "runtime name".to_owned()).as_str()
}
```

这样只初始化一次，后续调用复用同一值；无需每次 `Box::leak`。示例已用本机 `rustc --edition=2021` 编译运行。这里的 `static` 值也不会在程序退出时自动运行 `Drop`，所以它解决的是**所有权与重复泄漏**问题，并不提供退出时析构。[`OnceLock` 文档](https://doc.rust-lang.org/std/sync/struct.OnceLock.html)、[Rust Reference：static 项](https://doc.rust-lang.org/reference/items/static-items.html)。

若数据会反复生成、需要在运行中删除，或持有必须关闭的文件、连接等资源，就应保留拥有者（例如 `String`、`Box<T>`、`Arc<T>`）并设计合适的生命周期；不要把每个值都 leak。单纯遇到借用检查错误，也不是泄漏的理由。

## 依据

- `raw/rust-box-leak-use-cases-official-research-2026-11-05.md`：“查阅资料”与“核对结果”。
- `raw/rust-box-leak-string-chain-official-research-2026-11-05.md`：“核对结果”，说明 leak 如何消费 `Box` 及长期占用内存。

## 后续

- 若是某个具体 crate 要求 `&'static str`，应先核对该接口是否会长期保存引用，以及是否能改为持有 `String`、`Arc<str>` 或从单例借用。
