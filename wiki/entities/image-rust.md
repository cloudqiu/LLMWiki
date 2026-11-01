---
title: "image"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/image-rust-official-research-2026-11-01.md]
---

# image

## 用途与适用场景

以纯 Rust 编解码常见图像格式并处理图像缓冲。（[[image-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add image`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.25.10 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据发布文档公开 API 整理，需补足上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
let img = image::open("photo.png")?;
println!("{}x{}", img.width(), img.height());
```

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 相关库

[[jpeg-decoder-rust]]、[[fdeflate-rust]]、[[flate2-rust]]。

## 来源

- [[image-rust-official-research]]；本地查阅记录：`raw/image-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/image/latest/image/)；[crates.io](https://crates.io/crates/image)。
