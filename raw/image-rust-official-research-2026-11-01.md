# image 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：`image`。
- docs.rs 显示版本 0.25.10；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/image/latest/image/)；[crates.io 包页](https://crates.io/crates/image)。查阅日期：2026-11-01。

## 用途

以纯 Rust 编解码常见图像格式并处理图像缓冲。

## 典型入口

```rust
let img = image::open("photo.png")?;
println!("{}x{}", img.width(), img.height());
```

以上为根据公开 API 整理的最小片段，可能需要外层函数、依赖或平台条件；未编译运行。

## 身份与边界

- 发布文档可验证用途与公开 API，但包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 具体 feature、平台要求和兼容版本须按目标项目锁定版本核对。
