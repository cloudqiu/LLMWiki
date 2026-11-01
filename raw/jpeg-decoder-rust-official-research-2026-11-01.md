# jpeg-decoder 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：`jpeg-decorder`；核实后对应 `jpeg-decoder`，收件箱未改。
- docs.rs 显示版本 0.3.2；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/jpeg-decoder/latest/jpeg_decoder/)；[crates.io 包页](https://crates.io/crates/jpeg-decoder)。查阅日期：2026-11-01。

## 用途

解码 JPEG 图像及读取元数据。

## 典型入口

```rust
let file = std::fs::File::open("photo.jpg")?;
let mut decoder = jpeg_decoder::Decoder::new(std::io::BufReader::new(file));
let pixels = decoder.decode()?;
```

以上为根据公开 API 整理的最小片段，可能需要外层函数、依赖或平台条件；未编译运行。

## 身份与边界

- 发布文档可验证用途与公开 API，但包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- `jpeg-decorder` 无对应发布文档，按 `jpeg-decoder` 归档；实际依赖名待由 Cargo.lock 确认。
