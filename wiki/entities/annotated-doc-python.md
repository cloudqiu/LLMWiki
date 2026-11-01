---
title: "annotated-doc"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [python, library]
status: growing
sources: [raw/annotated-doc-python-official-research-2026-11-01.md]
---

# annotated-doc

## 用途与适用场景

用 typing.Annotated 在参数和属性类型旁写文档说明。（[[annotated-doc-python-official-research]]）

## 依赖与版本

- Python / PyPI；`python -m pip install annotated-doc`；发布名与 import 名可能不同。
- 2026-11-01 查阅 PyPI 页面显示版本：0.0.5；实际版本以目标项目 lock/requirements 文件为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。PyPI owner 或发布者本身不足以确认个人创建者及完整维护团队。

## 典型用法

以下片段根据发布页与公开 API 整理，需补足运行环境并按目标版本检验；**未在本机运行**。

```python
from typing import Annotated
from annotated_doc import Doc

def greet(name: Annotated[str, Doc("User name")]) -> str:
    return f"Hello, {name}"
```

## 关键限制

- Python 版本、可选依赖和实际 API 须按项目锁定版本核对。

## 相关库

[[fastapi-python]]、[[starlette-python]]、[[uvicorn-python]]、[[anyio-python]]、[[pydantic-python]]、[[annotated-types-python]]。

## 来源

- [[annotated-doc-python-official-research]]；本地查阅记录：`raw/annotated-doc-python-official-research-2026-11-01.md`。
- [PyPI 项目发布页](https://pypi.org/project/annotated-doc/)。
