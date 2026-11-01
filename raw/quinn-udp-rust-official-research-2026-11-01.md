# quinn-udp 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：`quinn-udp`。
- docs.rs 显示版本 0.6.3；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/quinn-udp/latest/quinn_udp/)；[crates.io 包页](https://crates.io/crates/quinn-udp)。查阅日期：2026-11-01。

## 用途

封装 QUIC 所需的 UDP 发送和接收能力。

## 典型入口

独立最小示例尚未从发布文档可靠确认；请沿文档 API 列表及所属上层 crate 使用。

## 身份与边界

- 包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 具体 feature、平台要求和兼容版本须按目标项目锁定版本核对。
