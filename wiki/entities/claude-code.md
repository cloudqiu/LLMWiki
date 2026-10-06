---
title: Claude Code
type: entity
entity_type: tool
created: 2026-10-01
updated: 2026-10-06
tags: [tool, llm, agent]
status: growing
sources: [raw/llm-wiki.md, raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md, raw/Windows Terminal：把黑框变好看.md]
---

# Claude Code

## 简介

Anthropic 的终端 AI 编程 agent；在 [[llm-wiki]] 模式中扮演「程序员」——直接读写 vault 中的 markdown 与 `CLAUDE.md`（schema 层），执行 ingest / query / lint 的日常维护。也是**本库的实际维护者**。

## 关键事实

- [[llm-wiki-pattern]] 将它列为模式适用的 agent 示例之一（与 Codex、OpenCode/Pi 并列），并注明其对 Claude Code 的 schema 文件即 `CLAUDE.md`。
- RUNOOB 教程（[[claude-code-obsidian-tutorial]]）的搭建流程：安装后，在 vault 目录运行 `claude` 启动会话，粘贴 gist 与提示词即可生成骨架（`CLAUDE.md` / `index.md` / `log.md` / 目录 / 模板）并完成首次摄入（教程 L45-60）。
- 直接读写本地文件、可执行 shell（如 git），适配「vault 即代码库」的用法。
- 安装说明：https://code.claude.com/docs/en/quickstart
- 教程将其与 Obsidian 并称「免费工具」（教程 L30）；实际计费方式（订阅 / API）**待核实**。

## 在本库中的角色

- 唯一的 wiki 维护者：所有 ingest / query / lint 操作的实际执行者（见 `CLAUDE.md` §0）。
- 与 [[obsidian]] 分工：「Obsidian 是 IDE；LLM 是程序员；wiki 是代码库」。
- **宿主环境**：作为终端 agent，它运行在某个 shell 里——Windows 上通常是 [[powershell]] 或 [[wsl]]，外壳多为 [[windows-terminal]]（→ [[command-line-interface]]、[[ai-era-command-line]]）。这是「环境层」第一次进入本库。

## 相关页面

- [[llm-wiki]]、[[llm-wiki-pattern]]、[[obsidian]]、[[claude-code-obsidian-tutorial]]

## 来源

- raw/llm-wiki.md（作为示例 agent 提及）
- raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md（搭建流程与定位）
- raw/Windows Terminal：把黑框变好看.md（作为终端内运行的 agent，间接涉及宿主外壳）
