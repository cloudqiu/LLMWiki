---
title: "Rust 开发环境安装（Windows|macOS|Linux）"
source: "https://mp.weixin.qq.com/s/J7Rbs4hrgvhZ4m82zy2qyw"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 2 篇上一篇我们介绍了为什么要学习 Rust，以及 Rust 的应用场景。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 7, 2026, 7:27 AM*

> 《Rust 编程实战》系列第 2 篇

上一篇我们介绍了为什么要学习 Rust，以及 Rust 的应用场景。

从这一篇开始，我们正式进入 Rust 的学习之旅。

在开始编写 Rust 程序之前，首先需要搭建开发环境。Rust 官方提供了统一的安装工具，无论是 Windows、macOS 还是 Linux，安装方式都非常简单。

本文将带你一步一步完成 Rust 开发环境的安装，并验证是否安装成功。

---

## Rust 官方推荐安装方式

Rust 官方推荐使用 **rustup** 来安装和管理 Rust。

`rustup` 是 Rust 官方提供的工具，它不仅可以安装 Rust，还可以：

- • 安装最新稳定版 Rust
- • 安装 Nightly（每日构建版）
- • 安装 Beta 版本
- • 管理多个 Rust 版本
- • 更新 Rust
- • 卸载 Rust
- • 安装不同目标平台（如 Windows、Linux、macOS、ARM）

相比手动下载安装包，使用 `rustup` 更方便，也更适合日常开发。

---

## Windows 安装 Rust

## 第一步：下载安装程序

访问 Rust 官方网站：

https://www.rust-lang.org/tools/install

点击 **Download rustup-init.exe** 下载 Windows 安装程序。

下载完成后，双击运行：

```
rustup-init.exe
```

安装界面通常会显示：

```
1) Proceed with standard installation (default)
2) Customize installation
3) Cancel installation
```

直接输入：

```
1
```

然后按 Enter。

安装程序会自动完成以下工作：

- • 安装 Rust 编译器
- • 安装 Cargo
- • 配置环境变量
- • 安装标准库

整个过程通常只需要几分钟。

---

## 第二步：验证安装

打开 PowerShell 或 CMD：

输入：

```
rustc --version
```

如果输出类似：

```
rustc 1.xx.x
```

说明安装成功。

再输入：

```
cargo --version
```

输出：

```
cargo 1.xx.x
```

说明 Cargo 也已经安装完成。

---

## macOS 安装 Rust

Rust 官方同样推荐使用 `rustup` 。

打开终端（Terminal），执行：

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

安装过程中会看到：

```
1) Proceed with standard installation
```

输入：

```
1
```

即可开始安装。

安装完成后，根据提示执行：

```
source "$HOME/.cargo/env"
```

或者重新打开终端。

然后验证：

```
rustc --version
```
```
cargo --version
```

如果能够正常输出版本号，则安装成功。

---

## Apple Silicon（M1/M2/M3）说明

如果你使用的是 Apple Silicon 芯片（M1、M2、M3 或更新型号），无需额外配置。

Rust 官方已经提供了原生 ARM64 支持。

查看当前架构：

```
uname -m
```

输出：

```
arm64
```

说明正在运行原生版本。

---

## Linux 安装 Rust

大多数 Linux 发行版都可以使用官方脚本安装。

执行：

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

安装完成后：

```
source "$HOME/.cargo/env"
```

然后验证：

```
rustc --version
```
```
cargo --version
```

---

## 查看 Rust 环境

查看 Rust 编译器版本：

```
rustc --version
```

查看 Cargo：

```
cargo --version
```

查看 rustup：

```
rustup --version
```

查看详细信息：

```
rustup show
```

例如：

```
Default host: aarch64-apple-darwin

installed toolchains
--------------------

stable-aarch64-apple-darwin

active toolchain
----------------

stable
```

---

## 更新 Rust

Rust 更新非常简单。

执行：

```
rustup update
```

更新完成后：

```
rustc --version
```

即可查看最新版本。

---

## 安装 Nightly 版本

Rust 有三个主要版本：

- • Stable（稳定版）
- • Beta（测试版）
- • Nightly（每日构建版）

安装 Nightly：

```
rustup toolchain install nightly
```

切换：

```
rustup default nightly
```

恢复稳定版：

```
rustup default stable
```

对于初学者，建议一直使用 Stable。

---

## 卸载 Rust

如果需要卸载：

```
rustup self uninstall
```

所有 Rust 组件都会被删除。

---

## 安装 Visual Studio Code

虽然任何文本编辑器都可以编写 Rust，但推荐使用 Visual Studio Code。

建议安装以下扩展：

- • rust-analyzer（智能提示、跳转定义、重构）
- • CodeLLDB（调试 Rust 程序）
- • Even Better TOML（编辑 Cargo.toml）
- • Error Lens（在编辑器中直接显示错误）

安装完成后，VS Code 会自动识别 Rust 项目，并提供代码补全、语法检查和格式化等功能。

---

## 第一个 Cargo 项目

安装完成后，可以创建第一个 Rust 项目。

执行：

```
cargo new hello_rust
```

进入项目：

```
cd hello_rust
```

运行：

```
cargo run
```

输出：

```
Hello, world!
```

恭喜，你已经成功运行了第一个 Rust 程序。

---

## 常见问题

## 提示 rustc: command not found

原因：

环境变量没有生效。

解决：

重新打开终端，或者执行：

```
source "$HOME/.cargo/env"
```

---

## 下载速度慢

可以临时配置国内镜像，例如使用社区提供的 Rust 镜像源，或为 Cargo 配置镜像仓库，以提升依赖下载速度。具体配置方式将在后续介绍 Cargo 时详细讲解。

---

## Cargo 下载依赖失败

可能原因包括：

- • 网络连接不稳定
- • 防火墙限制
- • 镜像配置错误

可以先确认网络环境，再检查 Cargo 的镜像配置是否正确。

---

## 小结

本文介绍了 Rust 在 Windows、macOS 和 Linux 上的安装方法，并完成了开发环境验证。

你已经掌握了：

- • 使用 rustup 安装 Rust
- • 安装 Cargo
- • 更新 Rust
- • 管理不同工具链
- • 创建第一个 Rust 项目
- • 配置推荐的开发工具

至此，我们已经完成了 Rust 开发环境的搭建。

下一篇文章，我们将编写第一个 Rust 程序，从 `Hello, World!` 开始，认识 Rust 项目的基本结构，并了解 Cargo 是如何组织和构建项目的。

![](https://wst.wxapp.tc.qq.com/161/20304/snscosdownload/SH/reserved/68a2beb40007712b291bfb7a2a0e1b15000000a000004f50?imageView2/1/w/800/h/800/q/50)

Rust编程很简单

假一赔三

7天无理由

¥76.3

已售15

![](https://res.wx.qq.com/shop/public/2024-10-17/fae7be51-beb6-4e61-aad8-4c1f7ccfab83.png)

机械工业出版社官方旗舰店

![](https://mmec.wxqcloud.qq.com.cn/shop/public/2026-07-13/1ade7f7a-528a-437d-a83b-b640764d8f70.png) ![](https://res.wx.qq.com/t/components/icons/base/arrow_down_regular.svg) 收起

使用手机微信

扫码了解商品信息

Rust 编程实战 · Table of Contents