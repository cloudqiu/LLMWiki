# Rust `Box::leak` 适用场景官方资料查阅记录（2026-11-05）

本文件是官方资料查阅笔记，不是官网原文副本。问题：什么情况下有意放弃 `Box` 的自动释放？

## 查阅资料

- Rust 标准库 `Box::leak`：https://doc.rust-lang.org/std/boxed/struct.Box.html
- Rust 标准库 `OnceLock`：https://doc.rust-lang.org/std/sync/struct.OnceLock.html
- Rust Reference，`static` 项的生命周期和析构：https://doc.rust-lang.org/reference/items/static-items.html
- Rustonomicon，资源泄漏与内存安全：https://doc.rust-lang.org/nomicon/leaking.html

## 核对结果

- `Box::leak` 消费 `Box<T>`，返回引用；标准库将它定位为数据有意存活到程序剩余时间的工具。内存若本应回收，就不适合泄漏。
- 适用场景是有界、通常只初始化一次的运行时数据，且某接口要求长期有效的引用、没有合适的拥有者可供该接口借用。具体注册器或外部 API 是否真的需要 `'static` 须看其契约；此处是由官方机制推导的设计场景。
- `OnceLock<String>` 可在 `static` 中一次初始化、之后返回借用，从而得到长期有效的引用而不用每次显式 `Box::leak`。`static` 自身也不在程序结束时运行 `Drop`；它是避免额外泄漏次数与集中所有权的替代方案，不是“会在退出时自动析构”的承诺。
- 若数据必须在程序运行中回收，应保留 `Box` / `String` / `Arc` 等拥有者，并让 API 接受合适的非 `'static` 借用或拥有值；不要因生命周期报错而泄漏。

## 验证

- 本机用 `rustc --edition=2021` 编译运行 `static OnceLock<String>` 返回 `&'static str` 的最小示例，断言通过。测试文件在临时目录，未加入知识库。
