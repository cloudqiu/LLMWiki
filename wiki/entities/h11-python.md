---
title: "h11"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [python, library]
status: stub
sources: [raw/h11-python-official-research-2026-11-01.md]
---

# h11

## 用途与适用场景

实现与网络 I/O 分离的 HTTP/1.1 协议状态机。（[[h11-python-official-research]]）

## 依赖与版本

- Python / PyPI；`python -m pip install h11`；发布名与 import 名可能不同。
- 2026-11-01 查阅 PyPI 页面显示版本：0.16.0；实际版本以目标项目 lock/requirements 文件为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。PyPI owner 或发布者本身不足以确认个人创建者及完整维护团队。

## 典型用法

独立最小 API 用法未从发布页可靠确认；从 [PyPI 项目页](https://pypi.org/project/h11/) 的文档链接继续核对。此页待补示例。

## 关键限制

- 这是协议状态机，不负责 socket I/O；通常通过上层 ASGI/HTTP 实现使用。

## 相关库

[[uvicorn-python]]、[[starlette-python]]。

## 来源

- [[h11-python-official-research]]；本地查阅记录：`raw/h11-python-official-research-2026-11-01.md`。
- [PyPI 项目发布页](https://pypi.org/project/h11/)。
