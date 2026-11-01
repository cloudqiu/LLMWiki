---
title: "fastapi"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [python, library]
status: growing
sources: [raw/fastapi-python-official-research-2026-11-01.md, raw/python-library-authors-official-research-2026-11-01.md]
---

# fastapi

## 用途与适用场景

用 Python 类型声明构建 HTTP API。（[[fastapi-python-official-research]]）

## 依赖与版本

- Python / PyPI；`python -m pip install fastapi`；发布名与 import 名可能不同。
- 2026-11-01 查阅 PyPI 页面显示版本：0.162.0；实际版本以目标项目 lock/requirements 文件为准。

## 作者与维护者

- 创建者：[[sebastian-ramirez]]，PyPI Credits 与其个人主页自述均支持。
- 当前维护：PyPI 列 `tiangolo` 为 maintainer；完整团队分工待验证。

## 典型用法

以下片段根据发布页与公开 API 整理，需补足运行环境并按目标版本检验；**未在本机运行**。

```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/")
def root():
    return {"message": "hello"}
```

## 关键限制

- Python 版本、可选依赖和实际 API 须按项目锁定版本核对。

## 相关库

[[starlette-python]]、[[uvicorn-python]]、[[anyio-python]]、[[pydantic-python]]、[[annotated-doc-python]]、[[annotated-types-python]]、[[slowapi-python]]、[[limits-python]]、[[orjson-python]]。

## 来源

- [[fastapi-python-official-research]]；本地查阅记录：`raw/fastapi-python-official-research-2026-11-01.md`。
- [PyPI 项目发布页](https://pypi.org/project/fastapi/)。
