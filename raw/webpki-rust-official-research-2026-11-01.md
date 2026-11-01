# webpki 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称与发布包名：`webpki`。
- docs.rs 显示版本 0.22.4；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/webpki/latest/webpki/)；[crates.io 包页](https://crates.io/crates/webpki)。查阅日期：2026-11-01。

## 用途

验证 Web PKI X.509 证书。

## 典型入口

独立最小示例尚未从发布文档可靠确认；请沿文档 API 列表及所属上层 crate 使用。

## 身份与边界

- 包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 这是单独发布的 `webpki` 包；不要与 `rustls-webpki` 包混为一谈，实际依赖版本须核对。
