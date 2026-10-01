---
title: Obsidian
type: entity
entity_type: tool
created: 2026-10-01
updated: 2026-10-01
tags: [tool, knowledge-management]
status: growing
sources: [raw/llm-wiki.md, raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md]
---

# Obsidian

## 简介

本地优先的 markdown 知识管理应用。本库即是一个 Obsidian vault；在 [[llm-wiki]] 工作流中承担「IDE」的角色——LLM 实时写入，用户实时浏览（循链接、看 graph view、读更新后的页面）。

## 关键事实（本库相关配置）

- 附件目录已设为 `raw/assets/`——剪藏文章后按 `Ctrl+Shift+D`（"Download attachments for current file"）把图片下载到本地，供 LLM 单独查看。注意：LLM 无法一次读取带内嵌图片的 markdown，先读文本、再看图。
- 模板文件夹已设为 `templates/`。
- **Graph view**：观察 wiki 形态的最佳方式——哪些是枢纽页、哪些是孤立页；也是 lint 的辅助手段。
- **Web Clipper**：浏览器扩展，网页一键转 markdown 存进 `raw/`——本库资料来源入口（[[claude-code-obsidian-tutorial|RUNOOB 教程]] L39 亦述）。
- 插件生态（原文提及）：Marp（markdown 幻灯片）、Dataview（对 frontmatter 做动态查询出表）——更多见下节「主题与插件」。

## 主题与插件（据 [[claude-code-obsidian-tutorial|RUNOOB 教程]]整理）

- **主题**（设置 → 外观 → 主题管理）：
  - Minimal —— 极简干净、高度可定制（github.com/kepano/obsidian-minimal）
  - AnuPpuccin —— 柔和 pastel 配色、暗色模式护眼
  - Blue Topaz —— 功能丰富、中文社区热门
  - Things —— 仿 Things 3 清爽风格
  - Sanctum —— 暖色调，适合长时间阅读写作
- **插件**（设置 → 第三方插件 → 社区插件）：
  - 图形与写作：Excalidraw（手绘/思维导图）、Kanban（看板）、Advanced Tables（表格增强）
  - 结构化：Templater（动态模板）、Dataview（frontmatter 查询出表，见 Backlog）、Tasks（跨笔记任务）
  - 导航与外观：Notebook Navigator（三栏浏览 + 日历）、Calendar（每日笔记）、Iconize（图标）、Style Settings（主题/字体自定义）
  - 版本管理：Git（Vault 自动备份，github.com/Vinzent03/obsidian-git）——本库目前直接用命令行 git（`CLAUDE.md` §6），未装此插件

## 在本库中的角色

- 用户侧界面（阅读/浏览/验证）+ 资料来源入口（Web Clipper）。

## 相关页面

- [[llm-wiki]]、[[llm-wiki-pattern]]、[[claude-code]]（协作 agent）、[[qmd]]

## 来源

- raw/llm-wiki.md（原文的实践描述与 "Tips and tricks" 一节）
- raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md（RUNOOB 教程：主题/插件清单一节）
