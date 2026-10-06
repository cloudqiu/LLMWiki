---
title: Windows Terminal
type: entity
entity_type: tool
created: 2026-10-06
updated: 2026-10-06
tags: [tool, terminal, windows, command-line]
status: growing
sources: [raw/Windows Terminal：把黑框变好看.md]
---

# Windows Terminal

## 简介

微软的现代**终端模拟器**（terminal emulator）：把 [[command-prompt|CMD]]、[[powershell]]、[[wsl]] 等 shell 装进同一窗口，以标签页与窗格（pane）组织会话。定位是**外壳而非替代**——它不改变任何命令的行为，只改变你与它们相处的方式（原文 L36-38）。

## 关键事实

- **统一入口**：一个窗口 + 标签页切换 + 分屏，替代「CMD / PowerShell / Ubuntu 三个黑框并排堆任务栏」（原文 L22-24、L50-59）。
- **可定制外观**：字体、配色、透明度、背景图，均通过 `settings.json` 配置（原文 L57）；默认设置已够用，原文建议先跑起来再慢慢调（L174-176）。
- **Windows 自带情况**：Win11 22H2 起随系统提供（WT ≥ 1.15）并成为默认命令行体验；Win10 需从 Microsoft Store 安装或 `winget install Microsoft.WindowsTerminal`（→ [[winget]]）。**已验证**（对照微软官方文档）。
- **默认终端应用**：设置 → 启动 → 默认终端应用程序 → 选 Windows Terminal；亦可经「设置 → 隐私和安全性 → 开发者选项」调整（原文 L178-187，与官方一致）。
- **系列上下文**：本篇是中文科普连载中的一讲，把它定位为「AI 时代命令行的统一入口」（原文 L32、L110-146）→ [[ai-era-command-line]]。

## 快捷键（原文表格，含核对）

原文把快捷键做成「命令卡片」并标注危险等级（原文 L98-108、L150-161；危险等级见 L152-160）。

| 操作 | 键位 | 原文危险等级 | 核对结果 |
| --- | --- | --- | --- |
| 新建标签页 | `Ctrl + Shift + T` | 🟢 | 与默认一致 |
| 切换标签页 | `Ctrl + Tab` | 🟢 | 与默认一致 |
| 左右分屏 | `Alt + Shift + D` | 🟢 | 实为 `DuplicatePaneAuto`——方向随当前窗格，**不保证左右** |
| 上下分屏 | `Alt + Shift + +` | 🟢 | **与当前默认不符**，见下方矛盾标注 |
| 关闭标签页 | `Ctrl + Shift + W` | 🟢 | 与默认一致 |
| 打开设置 | `Ctrl + ,` | 🟢 | 与默认一致 |
| 命令面板 | `Ctrl + Shift + P` | 🟢 | 与默认一致 |
| 复制 | `Ctrl + C` | 🟢 | **仅在选中内容时才是复制**，否则为中断信号 |
| 粘贴 | `Ctrl + V` | 🟡 | 旧版默认为 `Ctrl + Shift + V`；`Ctrl + V` 的启用版本待验证 |

> [!warning] 矛盾：分屏键位方向
> 原文（L103-104、L154-155）记 `Alt + Shift + +` 为「分屏（上下）」。
> 微软当前默认键位：`alt+shift+plus` → 向右复制窗格（左右并排）；`alt+shift+-` → 向下（上下堆叠）；`alt+shift+d` → 自动方向。
> 二者对「+ 号键产生哪个方向」的说法不一致。**本页以微软默认键位为准，原文记法存疑**；且 `+` 需主键盘区输入，小键盘的 `+` 不生效（官方文档明示）。
> 核对依据：Microsoft Learn《Windows Terminal → Actions》默认键位表（2026-10-06 经网络搜索核对；learn.microsoft.com 直接抓取被网络策略拦截，未能引原文页面）。

## 在本库中的角色

- 本库的维护者 [[claude-code]] 是终端 agent——Windows Terminal 是它可能的宿主外壳，也就是「人与 wiki 之间的界面」再往下一层的**环境层**。
- 与 [[command-line-interface]] 概念页配对：那页讲「终端 vs shell」的区分，本页是这一区分在 Windows 上的具体实现。

## 相关页面

- [[command-line-interface]]、[[command-prompt]]、[[powershell]]、[[wsl]]、[[winget]]、[[claude-code]]、[[ai-era-command-line]]
- 来源：[[windows-terminal-tutorial]]

## 来源

- raw/Windows Terminal：把黑框变好看.md（主来源）
- 核对补充：Microsoft Learn《Windows Terminal》安装与 Actions 文档（2026-10-06，经网络搜索）
