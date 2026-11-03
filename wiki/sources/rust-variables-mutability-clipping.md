---
title: "Rust 变量与不可变性：为什么默认不能修改变量？"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484423&idx=1&sn=a99f9a5ab204d5412299d1487965ce1f&chksm=f0e753b5c790daa30b06ef29317734208a1579445e24f6451f7ae763b35820c76472fae93896&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 变量与不可变性：为什么默认不能修改变量？.md"
format: article
---

# Rust 变量与不可变性：为什么默认不能修改变量？

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 6 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-11；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/Rust 变量与不可变性：为什么默认不能修改变量？.md`；[网页原址](https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484423&idx=1&sn=a99f9a5ab204d5412299d1487965ce1f&chksm=f0e753b5c790daa30b06ef29317734208a1579445e24f6451f7ae763b35820c76472fae93896&cur_album_id=4602071361631748097&scene=189#wechat_redirect)。

## 一句话概括

说明 `let` 默认不可变、`let mut` 可重新赋值，以及 shadowing 与类型推导。

## 核心要点

- `let` 绑定默认不可重新赋值，`let mut` 允许赋新值（“Rust 默认不可变”、“可变变量”）。
- 重复 `let x = ...` 是 shadowing，新绑定可以与旧绑定有不同类型；区别于 `mut` 修改同一绑定（“变量遮蔽”至“Shadowing 可以改变类型”）。
- 以类型推导和显式类型标注说明局部变量声明（“类型自动推导”、“显式指定类型”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[rust-interior-mutability]]。
- 待验证：“不可变对象天然线程安全”过于绝对；绑定不可变与对象的内部可变性、类型的 `Sync` 性质需要区分，参见 [[rust-interior-mutability]]。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
