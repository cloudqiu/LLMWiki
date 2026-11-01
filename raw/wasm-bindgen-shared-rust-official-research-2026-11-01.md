# wasm-bindgen-shared 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称与发布包名：`wasm-bindgen-shared`。
- docs.rs 显示版本 0.2.129；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/crate/wasm-bindgen-shared/latest)；[crates.io 包页](https://crates.io/crates/wasm-bindgen-shared)。查阅日期：2026-11-01。

## 用途

在 wasm-bindgen 与其 CLI 之间共享内部定义。

## 典型入口

独立最小示例尚未从发布文档可靠确认；请沿文档 API 列表及所属上层 crate 使用。

## 身份与边界

- 包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 这是 wasm-bindgen 内部依赖，通常不直接在应用中使用。
