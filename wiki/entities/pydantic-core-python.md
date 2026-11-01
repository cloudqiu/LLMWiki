---
title: "pydantic-core"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [python, library]
status: growing
sources: [raw/pydantic-core-python-official-research-2026-11-01.md]
---

# pydantic-core

## 用途与适用场景

实现 Pydantic 的底层验证和序列化核心。（[[pydantic-core-python-official-research]]）

## 依赖与版本

- Python / PyPI；`python -m pip install pydantic-core`；发布名与 import 名可能不同。
- 2026-11-01 查阅 PyPI 页面显示版本：2.50.2；实际版本以目标项目 lock/requirements 文件为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。PyPI owner 或发布者本身不足以确认个人创建者及完整维护团队。

## 典型用法

以下片段根据发布页与公开 API 整理，需补足运行环境并按目标版本检验；**未在本机运行**。

```python
from pydantic_core import SchemaValidator
validator = SchemaValidator({"type": "int"})
value = validator.validate_python("42")
```

## 关键限制

- 通常通过 Pydantic 使用；直接使用需核对 core schema 版本。

## 相关库

[[pydantic-python]]、[[annotated-types-python]]、[[typing-extensions-python]]、[[typing-inspection-python]]。

## 来源

- [[pydantic-core-python-official-research]]；本地查阅记录：`raw/pydantic-core-python-official-research-2026-11-01.md`。
- [PyPI 项目发布页](https://pypi.org/project/pydantic-core/)。
