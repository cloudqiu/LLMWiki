# certifi 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 PyPI 项目发布页整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱与 PyPI 发布名：`certifi`；Python import 名常用 `certifi`，实际入口以文档为准。
- [PyPI 项目发布页](https://pypi.org/project/certifi/)；查阅日期 2026-11-01；页面显示版本：2026.10.23。目标项目须以 requirements/lock 文件核对实际安装版本。

## 用途

提供 Mozilla 根证书 CA bundle 的 Python 路径。

## 典型入口

```python
import certifi
ca_bundle = certifi.where()
```

以上为按项目发布页与公开 API 整理的最小片段；需满足安装、外部服务或运行环境条件；未在本机运行。

## 身份与边界

- PyPI 维护者账号或发布者不能单独证明创建者及完整当前维护团队；两者待验证。
- CA bundle 有更新周期；安全使用时应按目标环境维护证书包。
