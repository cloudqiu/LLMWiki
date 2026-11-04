# Rust Sync、trait object 与跨线程智能指针：官方资料查阅记录

查阅日期：2026-11-04。本文件是官方资料的查阅笔记，不是官方原文副本。

## 官方来源

- Rust `Sync`：https://doc.rust-lang.org/std/marker/trait.Sync.html — `T: Sync` 当且仅当 `&T: Send`；`Cell`、`RefCell` 是非线程安全内部可变性的反例。
- Rust `Send`：https://doc.rust-lang.org/std/marker/trait.Send.html — 值可安全跨线程转移。
- Rust Reference trait object：https://doc.rust-lang.org/reference/types/trait-object.html — `dyn Trait` 是动态大小类型，须通过指针使用；对象有数据指针与 vtable；可附加 `Send`、`Sync` 等 auto trait 和生命周期 bound；基 trait 须 dyn compatible。
- Rust Book trait object：https://doc.rust-lang.org/book/ch18-02-trait-objects.html — 使用 trait object 统一处理不同具体类型，运行时动态分发。
- `Box<T>`：https://doc.rust-lang.org/std/boxed/struct.Box.html — `Box<T>: Send` 要求 `T: Send`；`Box<T>: Sync` 要求 `T: Sync`（忽略通常默认分配器的额外 bound）。Box 是独占所有权，不提供多所有者共享。
- `Rc<T>`：https://doc.rust-lang.org/std/rc/struct.Rc.html — 无条件 `!Send`、`!Sync`，单线程引用计数。
- `Arc<T>`：https://doc.rust-lang.org/std/sync/struct.Arc.html — 默认分配器下，`Arc<T>` 的 `Send` 和 `Sync` 都需要 `T: Send + Sync`；原子引用计数只解决共享所有权，不保证内部 T 的线程安全。
- `Mutex<T>`：https://doc.rust-lang.org/std/sync/struct.Mutex.html — `T: Send` 时 Mutex 同时 `Send`、`Sync`；互斥允许单次只有一个线程访问内部 T。
- `RwLock<T>`：https://doc.rust-lang.org/std/sync/struct.RwLock.html — `T: Send` 时 RwLock `Send`，`T: Send + Sync` 时 RwLock `Sync`；多读者可同时持有 `&T`。
- `Cell<T>`：https://doc.rust-lang.org/std/cell/struct.Cell.html — `T: Send` 时 Cell 可 `Send`，但不是 `Sync`；可说明“可转移”不等于“可共享”。

## 归纳边界

- `Box<T>` 用于独占转移；`Arc<T>` 用于多线程共享所有权；`Arc<Mutex<T>>` 用于共享可变状态；`Arc<RwLock<T>>` 用于多读少写且 T 满足相应条件；`Rc<RefCell<T>>` 只适合单线程共享可变状态。
- `dyn Trait` 本身不会自动携带 `Send` / `Sync` 约束。`Box<dyn Trait + Send>` 可转移所有权；`Arc<dyn Trait + Send + Sync>` 可在多个线程间共享；具体实现类型须满足声明的 auto trait。
- `Mutex<T>`、`RwLock<T>` 是同步原语，不等于引用计数智能指针；若多个线程都要拥有同一实例，通常外包 `Arc`。
- 示例仅以标准库为范围；Tokio 的异步锁还受任务调度及跨 `.await` 的要求影响，需按其文档另行核对。
