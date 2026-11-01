# digest 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 官方发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：digest。
- 已核实 crate：`digest`，docs.rs 显示版本 0.11.3；目标项目须以 Cargo.lock 核对实际使用版本。
- [官方发布文档](https://docs.rs/digest/latest/digest/)；[crates.io 包页](https://crates.io/crates/digest)。查阅日期：2026-11-01。

## 用途

定义密码学摘要算法的共用 trait。

## 典型入口

该 crate 的独立最小示例尚未从官方文档可靠确认；请沿文档 API 列表及所属上层 crate 使用。

## 身份与边界

- 发布文档可验证 crate 用途与公开 API，但单凭包所有者、仓库归属或发布账号不能确认个人创建者与当前维护者；两者待验证。
- 这是底层 trait crate；常由上层算法库重导出或封装。
