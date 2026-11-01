# icu_normalizer_data 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：`icu_normalizer_data`。
- docs.rs 显示版本 2.2.0；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/icu_normalizer_data/latest/icu_normalizer_data/)；[crates.io 包页](https://crates.io/crates/icu_normalizer_data)。查阅日期：2026-11-01。

## 用途

为 icu_normalizer 提供生成的 Unicode/CLDR 数据。

## 典型入口

该 crate 的独立最小示例尚未从发布文档可靠确认；请沿文档 API 列表及所属上层 crate 使用。

## 身份与边界

- 发布文档可验证用途与公开 API，但包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 此 crate 是生态中的组件；直接依赖前核对上层 crate 是否已重导出所需 API。
