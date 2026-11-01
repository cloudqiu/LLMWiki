---
title: "requests"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [python, library]
status: growing
sources: [raw/requests-python-official-research-2026-11-01.md]
---

# requests

## 用途与适用场景

以同步 API 发送 HTTP 请求。（[[requests-python-official-research]]）

## 依赖与版本

- Python / PyPI；`python -m pip install requests`；发布名与 import 名可能不同。
- 2026-11-01 查阅 PyPI 页面显示版本：2.34.2；实际版本以目标项目 lock/requirements 文件为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。PyPI owner 或发布者本身不足以确认个人创建者及完整维护团队。

## 典型用法

以下片段根据发布页与公开 API 整理，需补足运行环境并按目标版本检验；**未在本机运行**。

```python
import requests
response = requests.get("https://example.com", timeout=5)
response.raise_for_status()
```

## 关键限制

- Python 版本、可选依赖和实际 API 须按项目锁定版本核对。

## 相关库

[[urllib3-python]]、[[certifi-python]]、[[charset-normalizer-python]]、[[idna-python]]。

## 来源

- [[requests-python-official-research]]；本地查阅记录：`raw/requests-python-official-research-2026-11-01.md`。
- [PyPI 项目发布页](https://pypi.org/project/requests/)。
