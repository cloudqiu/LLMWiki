# anyio 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 PyPI 项目发布页整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱与 PyPI 发布名：`anyio`；Python import 名常用 `anyio`，实际入口以文档为准。
- [PyPI 项目发布页](https://pypi.org/project/anyio/)；查阅日期 2026-11-01；页面显示版本：4.15.1。目标项目须以 requirements/lock 文件核对实际安装版本。

## 用途

在 asyncio 或 Trio 上运行结构化异步并发代码。

## 典型入口

```python
import anyio

async def task():
    print("hello")

async def main():
    async with anyio.create_task_group() as group:
        group.start_soon(task)

anyio.run(main)
```

以上为按项目发布页与公开 API 整理的最小片段；需满足安装、外部服务或运行环境条件；未在本机运行。

## 身份与边界

- PyPI 维护者账号或发布者不能单独证明创建者及完整当前维护团队；两者待验证。
- Python 版本、可选依赖和实际 API 须按项目锁定版本核对。
