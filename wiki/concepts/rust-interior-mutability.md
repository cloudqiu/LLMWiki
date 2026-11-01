---
title: "Rust 内部可变性与 Cell 家族"
type: concept
created: 2026-11-01
updated: 2026-11-01
tags: [rust, interior-mutability]
status: growing
sources: ["raw/告别混淆！Rust Cell 家族：从 UnsafeCell 到 Cell、RefCell、OnceCell、LazyCell.md"]
---

# Rust 内部可变性与 Cell 家族

## 定义

内部可变性允许经共享引用修改内部状态；`UnsafeCell<T>` 是这一机制的底层原语，安全封装通过各自的访问规则维持 Rust 的内存安全。见 [[rust-cell-family-clipping]]、[Rust Reference](https://doc.rust-lang.org/reference/interior-mutability.html)。

## 选择线索

| 类型 | 访问方式 | 适合场景与限制 |
| --- | --- | --- |
| `Cell<T>` | 值复制、移动、替换 | 简单值；不能直接拿内部的普通引用。 |
| `RefCell<T>` | 运行时借用检查 | 单线程共享可变访问；借用冲突会 panic。 |
| `OnceCell<T>` | 一次初始化，之后共享读取 | 单线程惰性或延迟填值；线程安全版本见 `OnceLock`。 |
| `LazyCell<T>` | 首次访问执行初始化闭包 | 单线程惰性构造；线程安全版本见 `LazyLock`。 |
| `UnsafeCell<T>` | 底层原语 | 构建安全抽象时须自行保证别名和同步要求。 |

## 边界与争议

- `RefCell<T>` 将借用检查移至运行时，并未取消借用规则。可用 `try_borrow` / `try_borrow_mut` 处理冲突；[官方文档](https://doc.rust-lang.org/std/cell/struct.RefCell.html)。
- 原剪藏文对类型之间的实现依赖作简化描述；具体源码关系应按目标 Rust 版本核对，不能将五种类型视为单一继承链。原文 `raw/告别混淆！Rust Cell 家族：从 UnsafeCell 到 Cell、RefCell、OnceCell、LazyCell.md` 34–60 行。

## 相关页面

- [[rust-cell-family-clipping]]
