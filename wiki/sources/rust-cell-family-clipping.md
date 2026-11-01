---
title: "Rust Cell 家族：UnsafeCell、Cell、RefCell、OnceCell、LazyCell"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [rust, interior-mutability]
status: growing
sources: ["raw/告别混淆！Rust Cell 家族：从 UnsafeCell 到 Cell、RefCell、OnceCell、LazyCell.md"]
author: "锈铁匠（剪藏页署名）"
source_url: "https://mp.weixin.qq.com/s/7jZdthg4EHeOy8_Acf4iUQ"
raw_file: "raw/告别混淆！Rust Cell 家族：从 UnsafeCell 到 Cell、RefCell、OnceCell、LazyCell.md"
format: "article"
---

# Rust Cell 家族（剪藏）

## 来源信息

- 剪藏页面显示 2026-10-28 发表，署名锈铁匠；frontmatter 的 published 留空，原始发表时间待验证。
- 原文：`raw/告别混淆！Rust Cell 家族：从 UnsafeCell 到 Cell、RefCell、OnceCell、LazyCell.md`；[剪藏链接](https://mp.weixin.qq.com/s/7jZdthg4EHeOy8_Acf4iUQ)。
- 关键 API 另以 [Rust Reference](https://doc.rust-lang.org/reference/interior-mutability.html) 和 [std::cell](https://doc.rust-lang.org/std/cell/) 核对（2026-11-01）。

## 一句话概括

文章把五种 Cell 类型按底层原语、共享修改、运行时借用检查和一次/惰性初始化串起来。

## 核心要点

- `UnsafeCell<T>` 是 Rust 内部可变性的底层原语；安全封装仍需履行别名和借用规则。原文 16–22 行；Rust Reference。
- `Cell<T>` 通过值的移动、复制或替换提供共享引用下的修改，不提供内部值的普通共享引用；原文 24–32 行；std::cell。
- `RefCell<T>` 允许运行时借用检查，冲突的 `borrow()` / `borrow_mut()` 会 panic；原文 34–40 行；[官方文档](https://doc.rust-lang.org/std/cell/struct.RefCell.html)。
- `OnceCell<T>` 仅初始化一次，1.70.0 稳定；`LazyCell<T>` 首次访问时初始化，1.80.0 稳定；原文 44–60 行；[OnceCell](https://doc.rust-lang.org/std/cell/struct.OnceCell.html)、[LazyCell](https://doc.rust-lang.org/std/cell/struct.LazyCell.html)。

## 与既有知识的关系

- 派生 [[rust-interior-mutability]]。
- 原文 26 行借 Linux 使用 Rust 为安全性“背书”的说法是修辞，不是这些 API 正确性的证明；原文 40 行“实现 Borrow 和 BorrowMut 特征”不应替代对 `RefCell::borrow` / `borrow_mut` 方法与运行时规则的说明。
- 配图仍为远程微信资源，未保存本地；不据图片推断源码细节。

## 留给用户的讨论问题

- 后续是否要补 `std::sync::OnceLock`、`LazyLock` 与多线程边界的对照？
