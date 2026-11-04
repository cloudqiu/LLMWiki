---
title: "Rust 元组 Tuple 详解：组合不同类型的数据"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, rust-basics, tuples]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484463&idx=1&sn=cce568238bbbd8d525f6ae948bf88b8c&chksm=f0e7539dc790da8bf6bd0eb0bac8393fad65f57cdb3d4f5f78cd1527aa0e4752cd5db992d10f&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 元组 Tuple 详解：组合不同类型的数据.md"
format: article
---

# Rust 元组 Tuple 详解：组合不同类型的数据

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 16 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-21；未与网页在线核对。剪藏创建于 2026-11-04。
- 本地原文：`raw/Rust 元组 Tuple 详解：组合不同类型的数据.md`；原始链接见 frontmatter。

## 一句话概括

说明固定位置、可混合类型的元组如何访问、解构、模式匹配，以及何时改用有名字段的结构体。

## 核心要点

- 元组位置与类型固定，可用 `.0`、`.1` 等常量位置访问；不能像同类型数组那样动态索引或直接遍历（“元组长度和类型固定”至“为什么元组不能动态索引？”、“元组与数组的区别”）。
- 解构可绑定各元素，用 `_` 忽略、`..` 跳过一段；`_name` 仍绑定值，而 `_` 不绑定（“元组解构”至“可变解构”）。
- 函数可返回一个包含多个结果的元组，空输入可配合 `Option<(T, U)>`；元组模式也可与 `match`、`if let` 组合（“元组作为函数返回值”至“元组与 Option 组合”）。
- 单元素元组需要逗号 `(value,)`；空元组 `()` 是单元类型。元组整体能否 `Copy` 取决于元素；长期维护且字段有明确含义的数据宜用结构体（“单元素元组”至“元组与结构体的选择”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]]、[[rust-data-types-clipping]]、[[rust-match-patterns-clipping]]、[[rust-if-let-while-let-clipping]]、[[rust-array-clipping]]、[[rust-slice-clipping]]。
- 待验证：代码示例未在本次摄入时编译运行；正文署名与发表时间未在线核对。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
