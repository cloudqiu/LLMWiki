---
title: "jpeg-decoder"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/jpeg-decoder-rust-official-research-2026-11-01.md]
---

# jpeg-decoder

## 用途与适用场景

解码 JPEG 图像及读取元数据。（[[jpeg-decoder-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add jpeg-decoder`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.3.2 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据发布文档公开 API 整理，需补足上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
let file = std::fs::File::open("photo.jpg")?;
let mut decoder = jpeg_decoder::Decoder::new(std::io::BufReader::new(file));
let pixels = decoder.decode()?;
```

## 关键限制

- 收件箱写作 `jpeg-decorder`；按正式 crate `jpeg-decoder` 建页，实际依赖名待核对。

## 相关库

[[image-rust]]。

## 来源

- [[jpeg-decoder-rust-official-research]]；本地查阅记录：`raw/jpeg-decoder-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/jpeg-decoder/latest/jpeg_decoder/)；[crates.io](https://crates.io/crates/jpeg-decoder)。
