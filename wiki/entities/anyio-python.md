---
title: "anyio"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [python, library]
status: growing
sources: [raw/anyio-python-official-research-2026-11-01.md, raw/python-library-authors-official-research-2026-11-01.md]
---

# anyio

## 用途与适用场景

在 asyncio 或 Trio 上运行结构化异步并发代码。（[[anyio-python-official-research]]）

## 依赖与版本

- Python / PyPI；`python -m pip install anyio`；发布名与 import 名可能不同。
- 2026-11-01 查阅 PyPI 页面显示版本：4.15.1；实际版本以目标项目 lock/requirements 文件为准。

## 作者与维护者

- 作者：[[alex-gronholm]]，AnyIO PyPI Credits 明列；是否唯一创建者待验证。
- 当前维护：PyPI 列 `agronholm` 为多名 maintainer 之一；完整维护分工待验证。

## 典型用法

以下片段根据发布页与公开 API 整理，需补足运行环境并按目标版本检验；**未在本机运行**。

```python
import anyio

async def task():
    print("hello")

async def main():
    async with anyio.create_task_group() as group:
        group.start_soon(task)

anyio.run(main)
```

## 关键限制

- Python 版本、可选依赖和实际 API 须按项目锁定版本核对。

## 相关库

[[fastapi-python]]、[[starlette-python]]、[[uvicorn-python]]、[[pydantic-python]]、[[annotated-doc-python]]、[[annotated-types-python]]。

## 来源

- [[anyio-python-official-research]]；本地查阅记录：`raw/anyio-python-official-research-2026-11-01.md`。
- [PyPI 项目发布页](https://pypi.org/project/anyio/)。
