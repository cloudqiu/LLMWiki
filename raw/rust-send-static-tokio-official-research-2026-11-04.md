# Rust `Send + 'static` 与 Tokio 任务：官方资料查阅记录

查阅日期：2026-11-04。本文件是官方文档的查阅笔记，不是原文副本。代码示例未在本机编译。

## 官方来源与要点

- Rust 标准库 `Send`：https://doc.rust-lang.org/std/marker/trait.Send.html — 可以在线程边界间转移的类型；由编译器自动判断；`Rc` 非 `Send`，`Arc` 使用原子引用计数，但 `Arc<T>` 是否能传线程还取决于 `T`。
- Rust By Example `'static`：https://doc.rust-lang.org/rust-by-example/scope/lifetime/static_lifetime.html — `&'static T` 是引用生命周期；`T: 'static` 是类型约束，表示不包含较短生命周期的借用。拥有数据的 `String` 即使很快 drop，仍可满足此约束。
- Tokio Spawning 教程：https://tokio.rs/tokio/tutorial/spawning — `async move` 将拥有的数据移入任务；`tokio::spawn` 的任务可能跨线程调度，跨 `.await` 留存的状态需 `Send`；短暂使用 `Rc`、且在 `.await` 前离开作用域，可以成立。
- Tokio `spawn` API：https://docs.rs/tokio/latest/tokio/task/fn.spawn.html — 查阅时 1.54.1；签名要求 `F: Future + Send + 'static`，`F::Output: Send + 'static`。
- Tokio `spawn_local` API：https://docs.rs/tokio/latest/tokio/task/fn.spawn_local.html — `LocalSet` 或 LocalRuntime 中可运行 `!Send` Future，但仍要求 Future 和输出 `'static`。

## 解释边界

- `Send` 是跨线程安全转移，不等同 `Sync`（多线程共享引用）。`Arc` 不是任意 `T` 的自动跨线程许可证。
- `async move` 只改变捕获变量的所有权；若捕获的是借来的 `&T`，仍可能不满足 `'static`，须传入拥有的数据或合适的共享所有权。
- `tokio::spawn` 的 `Send` 限制不意味着任务一定迁移线程；这是 API 对可能迁移的任务提出的约束。
