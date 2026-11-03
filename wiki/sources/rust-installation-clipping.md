---
title: "Rust 开发环境安装（Windows/macOS/Linux）"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s/J7Rbs4hrgvhZ4m82zy2qyw"
raw_file: "raw/Rust 开发环境安装（WindowsmacOSLinux）.md"
format: article
---

# Rust 开发环境安装（Windows/macOS/Linux）

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 2 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-07；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/Rust 开发环境安装（WindowsmacOSLinux）.md`；[网页原址](https://mp.weixin.qq.com/s/J7Rbs4hrgvhZ4m82zy2qyw)。

## 一句话概括

介绍 rustup 在三个平台的安装、版本验证、工具链管理及第一个 Cargo 项目。

## 核心要点

- 以 rustup 安装工具链，随后用 `rustc --version`、`cargo --version`、`rustup show` 检查环境（“Rust 官方推荐安装方式”、“查看 Rust 环境”）。
- macOS/Linux 给出安装脚本及 shell 环境加载命令；Windows 给出安装程序路径（各平台安装小节）。
- 说明 stable、beta、nightly 与 `rustup update`，最后通过 `cargo new`、`cargo run` 验证（“更新 Rust”、“安装 Nightly 版本”、“第一个 Cargo 项目”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[rust-hello-world-clipping]]。
- 待验证：安装界面、平台前置条件、镜像源和卸载行为会随工具链更新；执行前应按官方安装页核对。文章中的安装步骤未在本次摄入时实机验证。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
