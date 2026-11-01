---
title: "jinja2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [python, library]
status: growing
sources: [raw/jinja2-python-official-research-2026-11-01.md]
---

# jinja2

## 用途与适用场景

用模板语法渲染文本和 HTML。（[[jinja2-python-official-research]]）

## 依赖与版本

- Python / PyPI；`python -m pip install jinja2`；发布名与 import 名可能不同。
- 2026-11-01 查阅 PyPI 页面显示版本：3.1.6；实际版本以目标项目 lock/requirements 文件为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。PyPI owner 或发布者本身不足以确认个人创建者及完整维护团队。

## 典型用法

以下片段根据发布页与公开 API 整理，需补足运行环境并按目标版本检验；**未在本机运行**。

```python
from jinja2 import Template
text = Template("Hello {{ name }}").render(name="Ada")
```

## 关键限制

- Python 版本、可选依赖和实际 API 须按项目锁定版本核对。

## 相关库

[[markupsafe-python]]。

## 来源

- [[jinja2-python-official-research]]；本地查阅记录：`raw/jinja2-python-official-research-2026-11-01.md`。
- [PyPI 项目发布页](https://pypi.org/project/jinja2/)。
