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
  - raw/rust-send-other-uses-official-research-2026-11-04.md
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

## `Send` 在 Tokio 之外的用法

`Send` 是标记 trait，没有要调用的方法。通常由编译器根据类型的成员自动判断；调用者通过 `T: Send` 约束声明“这里会把值交到另一线程”。[标准库定义](https://doc.rust-lang.org/std/marker/trait.Send.html)。

| 场景 | `Send` 保障什么 |
| --- | --- |
| `std::thread::spawn` | 移入新线程的闭包及其返回值都能安全跨线程转移；它们还要满足 `'static`。上文的 Tokio 任务与此相似。 |
| 跨线程 channel | 消息可从发送线程转移到接收线程。`channel::<T>()` 的构造签名本身没有 `T: Send`；当通道端点跨线程移动时才体现约束。 |
| 泛型 API | 例如 `fn submit<T: Send + 'static>(value: T)` 明确只接受可交给后台线程的值。 |
| trait object | `Box<dyn Job + Send>` 保留“装箱后仍可跨线程转移”的保证；仅写 `Box<dyn Job>` 不自动具有这项保证。 |

一个同步 Rust 的例子同时展示线程与 channel：

```rust
use std::{sync::mpsc, thread};

fn main() {
    let (tx, rx) = mpsc::channel::<String>();
    let worker = thread::spawn(move || {
        tx.send(String::from("完成")).unwrap();
    });

    println!("{}", rx.recv().unwrap());
    worker.join().unwrap();
}
```

这里 `String` 被送进 channel，再被接收线程取得；移动到线程里的 `tx` 也必须满足相应的线程安全约束。参见 [`thread::spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html) 与 [`mpsc::channel`](https://doc.rust-lang.org/std/sync/mpsc/fn.channel.html)。此片段已用本机 Rust 1.99.1 编译运行，输出“完成”。

### `Send` 与 `Sync` 的区别

`Send` 管**把值转移到别的线程**；`Sync` 管**多个线程共享 `&T`**。严格地说，`T: Sync` 当且仅当 `&T: Send`。[`Sync` 文档](https://doc.rust-lang.org/std/marker/trait.Sync.html)。`Rc<T>` 不适合跨线程；`Arc<T>` 的原子计数也不会自动让不安全的内部 `T` 变安全。常见共享可变状态需要额外同步，例如 `Arc<Mutex<T>>`；具体仍按 `T` 的约束判断。[`Arc` 文档](https://doc.rust-lang.org/std/sync/struct.Arc.html)。

一般不需要自己写 `unsafe impl Send`：编译器会自动推导。它是 `unsafe` trait，错误实现可能造成未定义行为；只有封装底层并发或 FFI 类型、且能完整证明跨线程安全时才考虑手动实现。[Rustonomicon](https://doc.rust-lang.org/nomicon/send-and-sync.html)。

## 依据

- `raw/rust-send-static-tokio-official-research-2026-11-04.md`「官方来源与要点」「解释边界」；[[tokio-rust]]。
- `raw/tokio-learning-guide-official-research-2026-11-04.md`「官方资料」；[[rust-tokio-systematic-learning-guide]]。
- `raw/rust-send-other-uses-official-research-2026-11-04.md`「官方资料」「归纳」：线程、channel、泛型接口及 `Send`/`Sync` 边界。
