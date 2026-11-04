---
title: "Rust 的 Send + 'static 怎么用？以 Tokio 任务为例"
type: answer
created: 2026-11-04
updated: 2026-11-04
tags: [rust, tokio, send, lifetimes, async]
status: growing
sources:
  - raw/rust-send-static-tokio-official-research-2026-11-04.md
  - raw/tokio-learning-guide-official-research-2026-11-04.md
---

# Rust 的 `Send + 'static` 怎么用？

> 归档自 2026-11-04 的查询，承接 [[rust-tokio-systematic-learning-guide]] 的 `tokio::spawn` 练习。

## 先看要求出现在哪里

[`tokio::spawn` 的签名](https://docs.rs/tokio/latest/tokio/task/fn.spawn.html)对任务 Future 和返回值都要求 `Send + 'static`：

```rust
F: Future + Send + 'static,
F::Output: Send + 'static,
```

- `Send`：这个值可以安全转移到另一线程。Tokio 可能在任务的 `.await` 前后换线程执行，所以跨 `.await` 保存的状态必须满足它。`Rc<T>` 通常不满足；`Arc<T>` 在内部 `T` 也符合线程安全约束时可以用。[标准库 Send](https://doc.rust-lang.org/std/marker/trait.Send.html)、[Tokio Spawning](https://tokio.rs/tokio/tutorial/spawning)。
- `T: 'static`：类型里没有会提前失效的借用；**不是**要求这个值存活到程序退出。拥有数据的 `String` 可以满足，即使任务一结束它就被释放。它与 `&'static str` 这种引用生命周期要分开理解。[Rust By Example](https://doc.rust-lang.org/rust-by-example/scope/lifetime/static_lifetime.html)。

## 修复常见的借用错误

下面任务默认借用 `name`，但任务可能在当前作用域结束后仍运行，因此不能满足 `'static`：

```rust
let name = String::from("Tokio");
tokio::spawn(async {
    println!("{name}");
});
```

让任务拥有 `String`，并等待任务结束：

```rust
#[tokio::main]
async fn main() {
    let name = String::from("Tokio");
    let task = tokio::spawn(async move {
        println!("{name}");
    });
    task.await.unwrap();
}
```

`move` 转移的是捕获的值；如果捕获的值本身是指向局部数据的 `&str`，仅加 `move` 仍不能让借用变成 `'static`。需要拥有字符串时可转成 `String`。上述示例根据官方公开 API 编写，未在本机编译。

## 父任务和子任务都要使用数据

共享所有权可用 `Arc`；克隆 `Arc` 句柄后把克隆件移入任务：

```rust
use std::sync::Arc;

#[tokio::main]
async fn main() {
    let data = Arc::new(vec![1, 2, 3]);
    let child_data = Arc::clone(&data);

    let task = tokio::spawn(async move {
        println!("子任务：{}", child_data.len());
    });
    println!("主任务：{}", data.len());
    task.await.unwrap();
}
```

`Arc` 只解决共享所有权；`Arc<Rc<_>>` 等内部含有非线程安全数据的组合，仍可能不满足 `Send`。

## 遇到 “future is not Send” 怎么查

检查编译器指出的 `.await`：哪些局部值在等待前创建、等待后仍会用？例如 `Rc` 跨 `.await` 存活会令整个 Future 不是 `Send`。如果只在 `.await` 前的一段独立作用域里使用并释放它，任务仍可能是 `Send`。需要长期保存 `!Send` 状态时，考虑在 `LocalSet` 或 LocalRuntime 中使用 [`spawn_local`](https://docs.rs/tokio/latest/tokio/task/fn.spawn_local.html)；它免除 `Send` 要求，但**仍要求 `'static`**。

## 一句话判断

把 `tokio::spawn(async move { ... })` 当成“这个任务可能比当前函数活得久，也可能换线程继续”：它要**拥有足够长久有效的数据**（`'static`），跨等待点保存的数据要**能安全跨线程转移**（`Send`）。任务不必真的活到程序结束，也不保证真的换线程。

## 依据

- `raw/rust-send-static-tokio-official-research-2026-11-04.md`「官方来源与要点」「解释边界」；[[tokio-rust]]。
- `raw/tokio-learning-guide-official-research-2026-11-04.md`「官方资料」；[[rust-tokio-systematic-learning-guide]]。
