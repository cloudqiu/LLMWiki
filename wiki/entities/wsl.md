---
title: WSL（Windows Subsystem for Linux）
type: entity
entity_type: tool
created: 2026-10-06
updated: 2026-10-06
tags: [tool, shell, linux, windows, ai-tooling]
status: stub
sources: [raw/Windows Terminal：把黑框变好看.md]
---

# WSL（Windows Subsystem for Linux）

## 简介

Windows 内的 Linux 子系统，原文定位为「Windows 里的真 Linux，跑 AI 工具」（原文 L20）。在 [[windows-terminal]] 的下拉菜单中以发行版名出现（如 Ubuntu）。

## 关键事实

- 原文列出的 WSL 侧命令生态：`curl`、`apt`、`python`、`ollama`（原文 L120）——即 AI 工具链的事实标准栖息地。
- 是本库 [[claude-code|Claude Code]] 在 Windows 上的一种常见运行方式（**待验证**：本库当前实际运行于何种 shell，见 `log.md` 的 setup 记录）。
- 发行版管理、文件系统互通（`/mnt/c`）、与 [[powershell]] 的边界——**待补充**。

## 在本库中的角色

- 「三世界命令」中最贴近 AI 的一支：本地模型（ollama）、Python 生态、Linux 工具链都在这一侧（原文 L120）。后续若摄入 Python 篇（→ [[ai-era-command-line]]），大概率要与此页联动。

## 相关页面

- [[windows-terminal]]、[[command-line-interface]]、[[powershell]]、[[command-prompt]]、[[windows-terminal-tutorial]]

## 来源

- raw/Windows Terminal：把黑框变好看.md（作为三环境之一被提及，无独立章节）
