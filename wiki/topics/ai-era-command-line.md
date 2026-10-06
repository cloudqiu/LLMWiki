---
title: AI 时代的命令行
type: topic
created: 2026-10-06
updated: 2026-10-06
tags: [command-line, ai-tooling, windows, tutorial-series]
status: growing
sources: [raw/Windows Terminal：把黑框变好看.md]
---

# AI 时代的命令行

## 概述

一个正在形成的主题：**非技术背景的人如何在自己的电脑上搭起可用的 AI 工具环境**。当前认知（来自唯一来源 [[windows-terminal-tutorial]]）：

- 起点不是「学会写命令」，而是**把命令放进一个不难受的壳里**——[[windows-terminal]] 的「统一入口」主张：不是新命令，是新窗口（原文 L162）。
- 关键概念区分是 [[command-line-interface|终端 ≠ shell]]：三个 shell（[[command-prompt|CMD]] / [[powershell]] / [[wsl]]）各自独立，AI 给的命令分属「三个世界」，切标签比判断该开哪个窗口更省事（原文 L114-124）。
- 本地 AI 工具（`ollama`、`python`、`curl`、`apt`）的现实栖息地是 [[wsl]] 一侧（原文 L120）。

## 脉络

- **第 0 层（前提）**— 用户已有 CMD / PowerShell / WSL 三个窗口，但彼此割裂、观感陈旧（原文 L16-28）。
- **第 1 层（外壳）**— [[windows-terminal]]：并置与分屏，外观可调 → 本页当前所在位置（[[windows-terminal-tutorial]]，系列「第二周末」）。
- **第 2 层（语言与环境，预告）**— 「为什么 AI 都爱写 Python？」：解释器、AI 脚本、生态 → 系列「第三周」第一站（原文 L193-205）。**尚未摄入**。
- 更远：本地模型 / agent 工具链在本机的落地路径（本库自身的 [[claude-code]] 即一例）。**待建**。

## 页面地图

| 页面 | 类型 | 一句话 |
| --- | --- | --- |
| [[windows-terminal-tutorial]] | 来源 | 本主题的首份来源：把黑框变好看 |
| [[windows-terminal]] | 实体 | 统一外壳：把三环境装进一个窗口 |
| [[command-line-interface]] | 概念 | 终端 ≠ shell：本主题的概念底座 |
| [[command-prompt]] | 实体 | 传统命令行（`.bat`、`dir`） |
| [[powershell]] | 实体 | Windows 现代命令行 / 系统管理 |
| [[wsl]] | 实体 | Windows 里的真 Linux，AI 工具栖息地 |
| [[winget]] | 实体 | 命令行装应用的入口 |
| [[guangying-niukou]] | 实体 | 本系列的中文科普出处（stub） |

## 开放问题

- **本库是否要承载这个主题？** 本库原有内容是 PKM / [[llm-wiki]]；本主题属于「操作系统与开发环境层」。若确认纳入，则它多半会与 [[personal-knowledge-management]] 的「环境层」形成上下位关系（先有能跑的终端，才有能跑的 agent）。若确认不纳入，建议整体迁出（先例：词汇系统迁往 LLMLangWiki，schema v1.7）。——*2026-10-06：用户未要求迁出，本主题**维持纳入**；「脉络」一节已按此调整（第 2 层起标为「尚未摄入」，不回补）。*
- **连载完整性** — *已决议（2026-10-06）：**不回补前文***。本主题的起点定为「第二周末」这一篇，前史留白不成问题。
- **「好看降低门槛」是否有据**：原文的经验主张（L142-146），本库无对照证据。
- **危险等级标注法**值得留意：原文用 🟢/🟡 给每条命令标注风险。这套做法能否借用到本库自己的文档规范（例如给 ingest / lint 类操作标注破坏性）？

## 来源

- raw/Windows Terminal：把黑框变好看.md
