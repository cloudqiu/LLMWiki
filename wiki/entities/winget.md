---
title: winget
type: entity
entity_type: tool
created: 2026-10-06
updated: 2026-10-06
tags: [tool, package-manager, windows, command-line]
status: stub
sources: [raw/Windows Terminal：把黑框变好看.md]
---

# winget

## 简介

Windows 的命令行包管理器（Windows Package Manager），用于从命令行安装应用。原文以 `winget install Microsoft.WindowsTerminal` 作为安装 [[windows-terminal]] 的示例（原文 L70-72）。

## 关键事实

- 与命令行生态天然搭配：安装命令可以直接让 AI 生成、粘贴执行，无需在浏览器里找安装包——这是「AI 给命令、你在终端里跑」闭环的一环（→ [[ai-era-command-line]]）。
- 官方文档写法为 `winget install --id Microsoft.WindowsTerminal -e`；原文的简写形式**待验证**（能否解析到同一包）。
- 其他用法（`winget search` / `upgrade` / `list`）——**待补充**。

## 在本库中的角色

- 「AI 时代命令行」这一主题里的**入口工具**：它让「换一个好用的外壳」这类建议变成一行可复制的命令。

## 相关页面

- [[windows-terminal]]、[[command-line-interface]]、[[windows-terminal-tutorial]]、[[ai-era-command-line]]

## 来源

- raw/Windows Terminal：把黑框变好看.md（仅一句示例）
