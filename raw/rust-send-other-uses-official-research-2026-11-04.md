# Rust Send 其他用法：官方资料查阅记录

查阅日期：2026-11-04。本文件是官方文档的查阅笔记，不是原文副本。

## 官方资料

- `Send` trait：https://doc.rust-lang.org/std/marker/trait.Send.html — 表示类型可安全跨线程转移；编译器通常自动实现；`Rc` 不满足。
- `Sync` trait：https://doc.rust-lang.org/std/marker/trait.Sync.html — 表示 `&T` 可安全跨线程共享；严格关系是 `T: Sync` 当且仅当 `&T: Send`。
- `std::thread::spawn`：https://doc.rust-lang.org/std/thread/fn.spawn.html — 闭包与返回值均要求 `Send + 'static`。
- `std::sync::mpsc::channel`：https://doc.rust-lang.org/std/sync/mpsc/fn.channel.html — `channel<T>()` 签名本身没有 `T: Send`；当 Sender/Receiver 要跨线程转移时，其类型约束会要求消息可安全跨线程转移。不要写成“channel 构造函数一律要求 Send”。
- `Arc`：https://doc.rust-lang.org/std/sync/struct.Arc.html — 原子引用计数只保障计数操作；`Arc<T>` 能否跨线程仍取决于 `T` 的 `Send` 和 `Sync`。
- Rustonomicon Send/Sync：https://doc.rust-lang.org/nomicon/send-and-sync.html — 两者为 unsafe auto marker traits；错误的手动 `unsafe impl` 可能造成未定义行为。普通业务类型通常依赖自动推导，不需要手写实现。

## 归纳

- `Send` 的主要场景：线程启动时移动闭包和结果、跨线程 channel 传消息、泛型函数公开并发能力约束、trait object 保留可跨线程特性，以及 Tokio 等执行器的任务要求。
- `Send` 管“转移”，`Sync` 管“共享引用”。可跨线程传递的类型不一定支持多个线程同时持有共享引用。
