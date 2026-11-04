---
title: "系统理解 Rust Sync、trait object 与跨线程智能指针"
type: answer
created: 2026-11-04
updated: 2026-11-04
tags: [rust, sync, send, traits, smart-pointers, concurrency]
status: growing
sources:
  - raw/rust-sync-trait-objects-smart-pointers-official-research-2026-11-04.md
  - raw/rust-send-other-uses-official-research-2026-11-04.md
---

# 系统理解 Rust `Sync`、trait object 与跨线程智能指针

> 归档自 2026-11-04 的查询，承接 [[rust-send-static-in-tokio]]。下文讨论标准库类型与默认分配器；自定义分配器还有自己的 trait bound。

## 1. `Sync` 的准确含义

`T: Sync` 表示把 **`&T` 共享引用**交给别的线程仍安全。精确定义是 `T: Sync` 当且仅当 `&T: Send`；与之相对，`T: Send` 表示把**拥有的 T 值**转移到别的线程安全。[`Sync` 文档](https://doc.rust-lang.org/std/marker/trait.Sync.html)、[`Send` 文档](https://doc.rust-lang.org/std/marker/trait.Send.html)。

| 类型 | Send | Sync | 为什么 |
| --- | --- | --- | --- |
| `String` | 是 | 是 | 拥有字节，可转移；共享 `&String` 只提供安全的只读访问。 |
| `Cell<i32>` | 是 | 否 | 可以整体转移；`set(&self, ...)` 没有跨线程同步，不能共享引用。 |
| `Mutex<Cell<i32>>` | 是 | 是 | `Mutex<T>` 在 `T: Send` 时提供独占访问，外部可安全共享。 |
| `Rc<T>` | 否 | 否 | 引用计数不是原子操作，与内部 T 无关。 |

`Sync` 不等于“值永远不可变”。`Mutex<T>`、`RwLock<T>` 和原子类型能在共享引用下安全改变状态，因为它们提供了同步。`Cell`/`RefCell` 只提供单线程内部可变性，不能共享到多个线程。[`Sync` 文档](https://doc.rust-lang.org/std/marker/trait.Sync.html)、[`Mutex` 文档](https://doc.rust-lang.org/std/sync/struct.Mutex.html)。

## 2. trait object 是什么

`dyn Trait` 把具体类型隐藏在统一接口后，调用方法时通过 vtable 在运行时分发。它本身大小不固定，所以实际写作 `&dyn Trait`、`Box<dyn Trait>`、`Arc<dyn Trait>` 等指针形式；基 trait 必须能成为 trait object（dyn compatible）。与 `T: Trait` 的编译期具体类型分发相比，它适合在同一容器或接口中处理多种实现。[Rust Reference](https://doc.rust-lang.org/reference/types/trait-object.html)、[Rust Book](https://doc.rust-lang.org/book/ch18-02-trait-objects.html)。

`dyn Trait` 只承诺 `Trait` 的方法，不自动承诺线程安全：

- `Box<dyn Trait + Send>`：隐藏的具体类型可安全**转移**到另一线程；Box 是独占所有权。
- `Arc<dyn Trait + Send + Sync>`：隐藏的具体类型满足跨线程转移与共享条件；多个线程可各持有一个 Arc 句柄。
- `Arc<Mutex<Box<dyn Trait + Send>>>`：需要通过锁共享一个可变的 trait object 时的常见组合；`Mutex` 保护访问，Box 保存动态大小的值。

`Send`、`Sync` 在这里是附加的 auto trait bound；被放入对象的具体实现必须满足它们。不要以为给外层套一个 `Arc` 就能把 `Rc` 或 `RefCell` 变成线程安全。[trait object 语法](https://doc.rust-lang.org/reference/types/trait-object.html)、[`Arc` 的线程安全条件](https://doc.rust-lang.org/std/sync/struct.Arc.html)。

### 一个跨线程的 trait object

```rust
use std::{sync::Arc, thread};

trait Service {
    fn name(&self) -> &'static str;
}

struct Greeter;
impl Service for Greeter {
    fn name(&self) -> &'static str { "hello" }
}

fn main() {
    let service: Arc<dyn Service + Send + Sync> = Arc::new(Greeter);
    let child = Arc::clone(&service);

    let worker = thread::spawn(move || child.name());
    assert_eq!(service.name(), "hello");
    assert_eq!(worker.join().unwrap(), "hello");
}
```

`Arc` 让主线程和子线程各持有一个句柄；`dyn Service` 让调用者不依赖具体的 `Greeter`；`Send + Sync` 约束确保隐藏的具体类型也满足跨线程要求。此示例已用本机 Rust 1.99.1 编译运行并通过断言。

## 3. 智能指针和同步原语怎么选

| 需求 | 选择 | 跨线程条件 |
| --- | --- | --- |
| 只把所有权交给另一线程 | `Box<T>`（很多时候直接移动 `T` 即可） | `T: Send`。Box 不提供共享所有权。 |
| 多线程共享只读或自身同步的对象 | `Arc<T>` | `T: Send + Sync`。 |
| 多线程共享可变数据，每次一个访问者 | `Arc<Mutex<T>>` | `T: Send` 即可让 `Mutex<T>` 可共享。 |
| 多读者并行、写者独占 | `Arc<RwLock<T>>` | `T: Send + Sync` 才能共享锁的读引用。 |
| 单线程共享所有权和内部可变性 | `Rc<RefCell<T>>` | `Rc` 始终 `!Send + !Sync`，不能跨线程。 |

这里 `Mutex` / `RwLock` 是同步原语，`Arc` 才负责多个线程共同拥有同一实例。`Arc<RefCell<T>>` 仍不安全，因为 Arc 只把**引用计数**做成原子操作，不会替内部的 `RefCell` 加锁。上述条件见 [`Box`](https://doc.rust-lang.org/std/boxed/struct.Box.html)、[`Arc`](https://doc.rust-lang.org/std/sync/struct.Arc.html)、[`Mutex`](https://doc.rust-lang.org/std/sync/struct.Mutex.html)、[`RwLock`](https://doc.rust-lang.org/std/sync/struct.RwLock.html) 的 trait 实现。

## 4. 排错顺序

1. 要**移动一个值**，还是让多个线程**持有同一份值**？前者查 `Send`，后者还需查 `Sync` 与所有权方式。
2. 编译器报 `T cannot be sent`：沿类型向内看是否有 `Rc`、借用、非 `Send` 成员；给 `Arc` 再套一层通常不能解决。
3. 报 `T cannot be shared`：检查内部的 `Cell`、`RefCell` 或 `dyn Trait` 是否缺 `Sync` bound；按访问方式选择 `Mutex` / `RwLock` 或消息传递。
4. trait object 报错时检查类型是否写成 `dyn Trait + Send + Sync`，以及具体实现是否满足这些 bound；还要单独处理 `thread::spawn` / `tokio::spawn` 的 `'static` 要求。详见 [[rust-send-static-in-tokio]]。

## 依据

- `raw/rust-sync-trait-objects-smart-pointers-official-research-2026-11-04.md`「官方来源」「归纳边界」。
- `raw/rust-send-other-uses-official-research-2026-11-04.md`「官方资料」；[[rust-send-static-in-tokio]]。
