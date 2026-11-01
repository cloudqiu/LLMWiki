# annotated-types 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 PyPI 项目发布页整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱与 PyPI 发布名：`annotated-types`；Python import 名常用 `annotated_types`，实际入口以文档为准。
- [PyPI 项目发布页](https://pypi.org/project/annotated-types/)；查阅日期 2026-11-01；页面显示版本：0.8.0。目标项目须以 requirements/lock 文件核对实际安装版本。

## 用途

为 typing.Annotated 提供范围、长度等约束元数据。

## 典型入口

```python
from typing import Annotated
from annotated_types import Gt
PositiveInt = Annotated[int, Gt(0)]
```

以上为按项目发布页与公开 API 整理的最小片段；需满足安装、外部服务或运行环境条件；未在本机运行。

## 身份与边界

- PyPI 维护者账号或发布者不能单独证明创建者及完整当前维护团队；两者待验证。
- Python 版本、可选依赖和实际 API 须按项目锁定版本核对。
