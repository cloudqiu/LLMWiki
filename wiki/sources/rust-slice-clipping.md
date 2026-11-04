---
title: "Rust 切片 Slice 详解：安全访问连续数据"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, rust-basics, slices]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484470&idx=1&sn=84610b55c727021a891db950dd0e8725&chksm=f0e75384c790da929457da33a7b93955ee0012e986407618439f026a4aaeaf5bc5f9f07db6b7&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 切片 Slice 详解：安全访问连续数据.md"
format: article
---

# Rust 切片 Slice 详解：安全访问连续数据

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 17 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-22；未与网页在线核对。剪藏创建于 2026-11-04。
- 本地原文：`raw/Rust 切片 Slice 详解：安全访问连续数据.md`；原始链接见 frontmatter。

## 一句话概括

用数组、`Vec` 和 UTF-8 字符串说明借用切片、范围边界、可变切片与安全访问。

## 核心要点

- `[T]` 是长度不定的切片类型，通常通过 `&[T]` 或 `&mut [T]` 使用；范围 `start..end` 不包含末端，`..=` 包含末端，切片借用原数据而不复制（“切片的类型”至“切片不会复制数据”）。
- 索引或范围无效时直接切片会 panic；`get(index)` / `get(range)` 返回 `Option`，适合处理不确定的边界（“访问切片元素”至“使用 get() 安全创建切片”）。
- 可变切片修改原集合的对应元素；函数参数 `&[T]` 可接受不同长度的数组和 `Vec` 借用，适合只读处理（“可变切片”至“数组、Vec 与切片”）。
- `&str` 是字符串切片；字符串范围以 UTF-8 字节边界计，非法字符边界会 panic。`chars()` 遍历 Unicode 标量值，`char_indices()` 给出对应字节位置（“字符串切片 &str”至“使用 char_indices() 获取字符位置”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]]、[[rust-array-clipping]]、[[rust-tuple-clipping]]、[[rust-functions-return-values-clipping]]。
- 待验证：示例未在本次摄入时编译运行；正文署名与发表时间未在线核对。`chars()` 的元素并不总等于用户感知的完整字符，处理字形簇需要另查资料。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
