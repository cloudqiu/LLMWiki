---
title: "Rust 数据类型详解：整数、浮点数、布尔、字符、元组和数组"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484427&idx=1&sn=88ebc40ede82d35519ef60071e8cf504&chksm=f0e753b9c790daaf352084f3cf5219a33fb3b85e3c356d3fe98576a36262ec1a6a15b66fc34a&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 数据类型详解：整数、浮点数、布尔、字符、元组和数组.md"
format: article
---

# Rust 数据类型详解：整数、浮点数、布尔、字符、元组和数组

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 7 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-12；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/Rust 数据类型详解：整数、浮点数、布尔、字符、元组和数组.md`；[网页原址](https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484427&idx=1&sn=88ebc40ede82d35519ef60071e8cf504&chksm=f0e753b9c790daaf352084f3cf5219a33fb3b85e3c356d3fe98576a36262ec1a6a15b66fc34a&cur_album_id=4602071361631748097&scene=189#wechat_redirect)。

## 一句话概括

概览 Rust 的整数、浮点、布尔、字符、元组与固定长度数组。

## 核心要点

- 把整数、浮点、bool、char 列为标量，把 tuple 与 array 列为复合类型（“Rust 数据类型分类”）。
- 说明整数 signed/unsigned 家族、`isize`/`usize`、`f32`/`f64`、Unicode `char`（相应类型小节）。
- 展示 tuple 的字段索引与解构、数组 `[T; N]`、类型推导、显式转换（“元组”至“类型转换”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[rust-functions-return-values-clipping]]。
- 待验证：`as` 转换可能截断或改变数值，文中 `a as u32 + b` 对负数尤其不宜直接照搬；常量数组越界示例也不宜概括为必定“运行时 panic”。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
