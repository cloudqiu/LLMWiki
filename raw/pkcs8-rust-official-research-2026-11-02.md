# pkcs8 官方资料查阅记录

> 2026-11-02 查阅 crates.io 官方包元数据；本文为研究笔记，不是官方原文副本。API 示例未在本机运行。

## 名称与版本

- 收件箱名称：`pkcs8`。
- crates.io 发布名：`pkcs8`；显示稳定版本：0.11.0。项目实际版本以 Cargo.lock 为准。
- [官方包页](https://crates.io/crates/pkcs8)；[注册表 API](https://crates.io/api/v1/crates/pkcs8)；[发布文档](https://docs.rs/pkcs8/latest/pkcs8/)。

## 用途

- 官方英文摘要：Pure Rust implementation of Public-Key Cryptography Standards (PKCS) #8: Private-Key Information Syntax Specification (RFC 5208), with additional support for PKCS#8v2 asymmetric key packages (RFC 5958)
- 中文概括：此 crate 提供上述功能；更具体的适用场景与 API 入口待依据发布文档核实。

## 典型入口

- 安装：`cargo add pkcs8`。
- 独立最小调用示例待按对应版本的文档补齐；未编译运行。

## 身份与边界

- 官方元数据列出的仓库：https://github.com/RustCrypto/formats。仓库归属不等于创建者或完整维护者名单。
- 创建者、当前维护者：待官方证据核实。
- feature、平台与实际 API 需按目标项目锁定版本核对。
