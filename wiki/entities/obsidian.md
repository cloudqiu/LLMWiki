---
title: Obsidian
type: entity
entity_type: tool
created: 2026-10-01
updated: 2026-10-01
tags: [tool, knowledge-management]
status: growing
sources: [raw/llm-wiki.md]
---

# Obsidian

## 简介

本地优先的 markdown 知识管理应用。本库即是一个 Obsidian vault；在 [[llm-wiki]] 工作流中承担「IDE」的角色——LLM 实时写入，用户实时浏览（循链接、看 graph view、读更新后的页面）。

## 关键事实（本库相关配置）

- 附件目录已设为 `raw/assets/`——剪藏文章后按 `Ctrl+Shift+D`（"Download attachments for current file"）把图片下载到本地，供 LLM 单独查看。注意：LLM 无法一次读取带内嵌图片的 markdown，先读文本、再看图。
- 模板文件夹已设为 `templates/`。
- **Graph view**：观察 wiki 形态的最佳方式——哪些是枢纽页、哪些是孤立页；也是 lint 的辅助手段。
- 插件生态（原文提及）：Web Clipper（网页 → markdown，收进 raw/）、Marp（markdown 幻灯片）、Dataview（对 frontmatter 做动态查询出表）。

## 在本库中的角色

- 用户侧界面（阅读/浏览/验证）+ 资料来源入口（Web Clipper）。

## 相关页面

- [[llm-wiki]]、[[llm-wiki-pattern]]、[[qmd]]

## 来源

- raw/llm-wiki.md（原文的实践描述与 "Tips and tricks" 一节）
