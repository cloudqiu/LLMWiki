---
title: "Rust Vec 动态数组详解：创建、增删、遍历与排序"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, rust-basics, collections]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484482&idx=1&sn=ae6a33e13c5d5caf5d145e1bf5ace454&chksm=f0e753f0c790dae660d76f944291bce465f73912924a78ac1c6c2e68d7667184073b94481639&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust Vec 动态数组详解：创建、增删、遍历与排序.md"
format: article
---

# Rust Vec 动态数组详解：创建、增删、遍历与排序

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 19 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-24；未与网页在线核对。剪藏创建于 2026-11-04。
- 本地原文：`raw/Rust Vec 动态数组详解：创建、增删、遍历与排序.md`；原始链接见 frontmatter。文末有剪藏带入的商品广告，不作为教程内容。

## 一句话概括

介绍可增长的同类型集合 `Vec<T>` 的增删改查、容量、排序去重，以及借用和所有权边界。

## 核心要点

- `vec![]`、`Vec::new()` 和 `Vec::with_capacity()` 建立动态集合；`len()` 是元素数，`capacity()` 是当前无需重新分配即可容纳的数量，具体增长策略是实现细节（“使用 vec! 宏创建 Vec”至“使用重复值创建 Vec”、“len() 与 is_empty()”至“预留和释放容量”）。
- `push()` / `pop()` 操作末端，`insert()` / `remove()` 移动后续元素；不需保持顺序时 `swap_remove()` 可更快删除。索引可能越界，`get()` 返回 `Option`（“使用 push() 添加元素”至“使用 get() 安全访问”）。
- `sort()` 排序；浮点数使用 `partial_cmp()` 时要处理 `NaN`。`dedup()` 仅去相邻重复值，若排序后去重会改变原顺序（“排序 Vec”至“去除重复元素”）。
- `Vec<T>` 可作为 `&[T]` 传给只读函数；对 `Vec<String>` 的元素，可借用、克隆或通过 `remove()` 移出。队列频繁从头删除时，文中建议考虑 `VecDeque`（“Vec 与切片”至“数组、Vec 与切片的区别”、“实战：简单任务队列”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]]、[[rust-array-clipping]]、[[rust-slice-clipping]]、[[rust-string-str-clipping]]、[[rust-if-let-while-let-clipping]]。
- 待验证：代码示例未在本次摄入时编译运行；正文署名和发表时间未在线核对。浮点排序示例用 `partial_cmp(...).unwrap()`，仅适用于已排除 `NaN` 的数据，不应直接套用到任意输入。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]、[[rust-array-clipping]]。
