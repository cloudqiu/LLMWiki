---
title: "Crate List（blessed.rs）"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, crates, recommendations]
status: growing
author: "blessed.rs（剪藏未列个人作者）"
source_url: "https://blessed.rs/crates"
raw_file: "raw/Crate List.md"
format: article
---

# Crate List（blessed.rs）

## 来源信息

- 作者 / 出处：blessed.rs 的 crate 清单；剪藏未列个人作者或发布日期。
- 获取日期：剪藏创建于 2026-11-04；网页现状未在线核对。
- 本地原文：`raw/Crate List.md`；原始链接见 frontmatter。

## 一句话概括

按使用场景编排 Rust crate 候选，并在若干领域给出选择条件和替代项。

## 核心要点

- 清单涵盖常见用途、数学科学、FFI、密码学、网络、数据库、CLI、并发和图形；这些分类适合按任务找候选，而不是把推荐名当成已核实的依赖声明（各 `###` 分类）。
- 同一用途常列多种选择：日期时间对比 jiff、[[time-rust|time]]、[[chrono-rust|chrono]]；HTTP 请求列 [[reqwest-rust|reqwest]] 与 ureq；正则列 regex 与 fancy-regex；异步、数据库和图形也按子场景细分（“Common / General”、“Networking”、“Databases”、“Graphics”）。
- 多数条目指向 lib.rs 和 docs.rs，可作为继续查找官方项目文档的入口；清单中的偏好与维护状态仍需逐个复核。

## 与既有知识的关系

- 关联：[[rust-crate-selection]]、[[time-rust]]、[[chrono-rust]]、[[reqwest-rust]]。
- 待验证：剪藏没有发布日期；例如 chrono 的“soft-deprecated”标注及各库维护状况会变化，应沿其链接查当前项目公告，不能只凭本页做选型结论。清单中的作者评价不是 crate 创建者、维护者或 API 用法的证据。

## 由本来源派生 / 更新的页面

- [[rust-crate-selection]]。
