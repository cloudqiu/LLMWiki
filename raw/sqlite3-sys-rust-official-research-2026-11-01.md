# sqlite3-sys 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：`sqlite3-sys`。
- docs.rs 显示版本 0.18.2；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/sqlite3-sys/latest/sqlite3_sys/)；[crates.io 包页](https://crates.io/crates/sqlite3-sys)。查阅日期：2026-11-01。

## 用途

提供 SQLite C API 的底层 Rust 绑定。

## 典型入口

独立最小示例尚未从发布文档可靠确认；请沿文档 API 列表及所属上层 crate 使用。

## 身份与边界

- 包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 具体 feature、平台要求和兼容版本须按目标项目锁定版本核对。
