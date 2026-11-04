---
title: "Rust 数组 Array 详解：定义、访问、遍历与切片"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, rust-basics, arrays]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484459&idx=1&sn=5d58aace2c52ded990f5b3a74648b4d6&chksm=f0e75399c790da8f52a29f25515b6016e8072a6a41182581aeeeb8959e890c01019ad0b4244c&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 数组 Array 详解：定义、访问、遍历与切片.md"
format: article
---

# Rust 数组 Array 详解：定义、访问、遍历与切片

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 15 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-20；未与网页在线核对。剪藏创建于 2026-11-04。
- 本地原文：`raw/Rust 数组 Array 详解：定义、访问、遍历与切片.md`；原始链接见 frontmatter。

## 一句话概括

用固定长度、同类型的数组引入 Rust 集合数据，讲解索引、迭代、切片及与 `Vec` 的取舍。

## 核心要点

- 数组类型为 `[T; N]`，长度属于类型；可用 `[value; N]` 重复初始化，`mut` 允许修改元素，但不能增减元素（“数组的基本语法”至“使用重复值初始化数组”、“修改数组元素”）。
- 索引从零开始；直接越界访问会 panic，`get()` 返回 `Option`，`first()` / `last()` 可处理边界位置（“访问数组元素”至“索引访问与 get() 的区别”）。
- `for`、`iter()`、`iter_mut()`、`enumerate()` 展示值、借用、可变借用和索引的遍历方式；`&numbers[start..end]` 借用连续范围，不复制元素，但无效范围仍会 panic（“使用 for 遍历数组”至“使用 fill() 填充数组”、“数组切片 Slice”至“切片也可能越界”）。
- 固定长度数组参数只接受对应 `[T; N]`；只读且无固定长度要求的函数可使用 `&[T]`。动态增删元素的场景使用 `Vec<T>`（“数组作为函数参数”至“使用切片作为函数参数”、“数组与 Vec 的区别”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]]、[[rust-data-types-clipping]]、[[rust-loops-clipping]]、[[rust-tuple-clipping]]、[[rust-slice-clipping]]、[[rust-vec-clipping]]。
- 待验证：文章的代码示例没有在本次摄入时编译运行；关于数组与 `Vec` 存储位置的简化表述不宜当作绝对规则。正文署名与发表时间未在线核对。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
