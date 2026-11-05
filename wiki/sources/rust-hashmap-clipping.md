---
title: "Rust HashMap 详解：键值存储、查询、更新与统计"
type: source
created: 2026-11-05
updated: 2026-11-05
tags: [rust, rust-basics, collections]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484488&idx=1&sn=32f7c0080926ab4747f259c9e51e6a57&chksm=f0e753fac790daec218dc8f6fef5d899934c49dbd33e9eb108ff8b0914bb4b5529d86cc5accf&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust HashMap 详解：键值存储、查询、更新与统计.md"
format: article
---

# Rust HashMap 详解：键值存储、查询、更新与统计

## 来源信息

- 《Rust 编程实战》第 20 篇；正文显示 2026-07-25，剪藏于 2026-11-05。原文件的 `author`、`published` 字段为空；署名及日期未在线核对。
- 原文：`raw/Rust HashMap 详解：键值存储、查询、更新与统计.md`；网页地址见 frontmatter。

## 一句话概括

介绍标准库 `HashMap<K, V>` 的键值访问、`entry()` 更新、所有权与无序遍历，并用库存和词频案例串联。

## 核心要点

- `std::collections::HashMap` 按键存取；`insert()` 覆盖旧值并返回 `Option<V>`，`get()` 返回 `Option<&V>`，`get_mut()` 可取得可变引用，`remove()` 删除并返回值（“导入 HashMap”至“使用 remove() 删除数据”）。
- `entry(key).or_insert(default)` 适合缺失时插入默认值及计数；`or_insert_with()` 仅在缺失时计算默认值（“使用 entry() 插入默认值”至“or_insert_with()”）。
- 插入拥有所有权的 `String` 会移动它；借用作为键和值时必须满足生命周期。`String` 键可用 `&str` 查询；遍历次序无保证（“遍历 HashMap”、“HashMap 的所有权”至“String 键的查询”）。
- `Vec` 保持元素顺序并用数字索引；`HashMap` 按键查询，适合库存、索引和计数（“HashMap 与 Vec 的区别”至三个“实战”小节）。

## 与既有知识的关系

- 接续 [[rust-vec-clipping]]；`get()` 的缺失分支接 [[rust-option-clipping]] 和 [[rust-if-let-while-let-clipping]]。学习顺序见 [[rust-programming-basics]]。
- 待验证：示例未在本次摄入时编译；来源署名和发表时间未在线核对。词频案例的输出顺序不能当成稳定结果；文中的 `HashMap` 与 `Vec` 对比只是入门概括。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
