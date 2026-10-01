---
title: "Claude Code + Obsidian 还能这么玩，从零搭一套会自己整理的知识库"
type: source
created: 2026-10-01
updated: 2026-10-01
tags: [knowledge-management, llm, tutorial]
status: growing
author: RUNOOB
source_url: https://mp.weixin.qq.com/s/ySiAUMffzBDMgsqyMft_PA
raw_file: raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md
format: article
---

# Claude Code + Obsidian 还能这么玩，从零搭一套会自己整理的知识库

## 来源信息

- 作者 / 出处：微信公众号「RUNOOB」（→ [[runoob]]；与编程教程站 runoob.com 的关系**待验证**）
- 发布 / 获取日期：发布日期原文未署；2026-10-01 剪藏入库（首剪受微信反爬影响仅获空壳文件，同日重剪修复，完整正文以重剪版为准）
- 本地文件：`raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md`
- 原始链接：https://mp.weixin.qq.com/s/ySiAUMffzBDMgsqyMft_PA
- 形式：中文教程长文——前半讲模式与从零搭建步骤，后半附 Obsidian 主题/插件清单
- 图片：正文含 15 张远程截图（`mmbiz.qpic.cn`），**未下载到本地**；文字层已自足

## 一句话概括

> 一篇把 Karpathy [[llm-wiki]] 模式落成可复现步骤的中文教程：装 Obsidian + [[claude-code|Claude Code]] + Web Clipper，把 gist 贴给 agent 生成骨架，此后「扔资料 → `ingest this` → 看它干活」。

## 核心要点

- **模式转述**：与 [[llm-wiki-pattern]] 一致——「Obsidian 是 IDE，LLM 是程序员，Wiki 是代码库」；用户只负责扔资料，阅读/总结/分类/建链/发现冲突/更新旧知/维护索引全交给 Claude Code（原文 L12-18）。
- **RAG 对照**：复述 [[llm-wiki-vs-rag]] 的核心论点——传统 RAG 每次提问重新检索拼凑，LLM Wiki 一次性编译、持续维护、知识复利（原文 L22）。
- **从零搭建流程**（教程主线）：
  1. 安装三个工具：Obsidian、Claude Code、Obsidian Web Clipper（原文 L28-39）；
  2. 新建 vault 文件夹，在其中打开终端运行 `claude`，粘贴 gist 链接 + 脚手架提示词，由 agent 生成完整目录结构、`CLAUDE.md`、`index.md`、`log.md`、模板，并把 gist 本身作为第一份资料摄入（原文 L45-60）——本库的 setup 即这一流程的实例（见 `log.md`）；
  3. 用 Web Clipper 把网页存成 markdown 进 `raw/`（教程用 `raw/articles/`，见「实现差异」）；
  4. 输入 `ingest this`，观察全流程跑通（原文 L78-86）。
- **架构复述**：三层（Raw sources 不可变 / Wiki 由 AI 维护 / Schema 即 `CLAUDE.md` 共同演化）+ 辅助文件（index.md、log.md）+ 三循环（ingest / query / lint，「一篇文章可能触碰 10-15 个页面」）（原文 L90-106）。
- **Obsidian 主题与插件清单**（教程后半，工具种草；完整清单已入库 [[obsidian]]）：
  - 主题 5 款：Minimal（极简可定制）、AnuPpuccin（柔和 pastel）、Blue Topaz（中文社区热门）、Things（仿 Things 3）、Sanctum（暖色调长阅读）；
  - 插件 11 款：Excalidraw、Templater、Dataview、Tasks、Advanced Tables、Notebook Navigator、Calendar、Kanban、Git、Style Settings、Iconize。

## 关键细节（值得引用的原文片段）

<!-- 引用时注明在 raw 文件中的大致位置（行号或小节名） -->

- L15：「Obsidian 是 IDE，LLM 是程序员，Wiki 是代码库。」
- L18：「我们只负责不断往 Obsidian里面扔东西，文章、PDF、论文、截图、会议记录、ChatGPT 对话…… 剩下的阅读、总结、分类、建立链接、发现冲突、更新旧知识、维护索引，全部交给 Claude Code。」
- L22：「传统 RAG 是每次提问都从原始文件重新检索拼凑答案，LLM Wiki 则是让 AI 一次性编译并持续维护一个结构化的、互相链接的 Markdown 知识库，知识会复利增长，而不是每次从零开始。」
- L39：「Obsidian Web Clipper 可以一键把网页转成 Markdown 存进 raw/。」
- L48（脚手架提示词，可直接复用）：「这是 Andrej Karpathy 的 LLM Wiki 模式：https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f。请把它实现成我的个人知识库： 创建完整的目录结构、CLAUDE.md、index.md、log.md 和模板文件， 并把这份 gist 本身当作第一份要摄入的资料。」
- L67（教程生成的目录树）：`raw/{articles, papers, assets}`、`wiki/{entities, concepts, sources, synthesis}`、`output/`。
- L84：「读原文 → 和你讨论要点 → 在 `wiki/sources/` 写摘要页 → 更新相关实体页和概念页 → 补交叉链接 → 更新 index.md → 在 log.md 记一笔。」

## 与既有知识的关系

- **印证**：本教程是 [[llm-wiki-pattern]] 的忠实中文转述与操作化；对 [[llm-wiki]]、[[llm-wiki-vs-rag]] 均为支持性来源，无矛盾。
- **实现差异**（非矛盾——gist 明言结构是示例性的）：教程的目录变体为 `raw/` 子目录化（articles / papers）、wiki 用 `synthesis/` 收综合页、另设 `output/` 放查询结果与 lint 报告；本库为 `raw/` 平铺 + wiki 六类目录（topics / comparisons / answers，无 output）。两种实例化并存，见讨论问题。
- **传播证据**：模式已从英语 idea file（[[llm-wiki-pattern]]）进入中文社区教学；本库与该教程是同一模式的两次独立实例化。
- **存疑 / 待验证**：
  - 「Karpathy 于 2026 年 4 月提出此模式」——教程说法（L12），未见一手日期，**待验证**（gist 本身未署日期；其 log 格式示例用的是 `2026-04-02`）。
  - 「OpenAI 联合创始人」头衔亦为二手转述 → [[andrej-karpathy]]。
  - 原文称 Obsidian 与 Claude Code 均为「免费工具」（L30）；Claude Code 具体计费方式**待核实** → [[claude-code]]。
  - 作者「RUNOOB」与 runoob.com（菜鸟教程）的关系**待验证** → [[runoob]]。

## 由本来源派生 / 更新的页面

- 来源摘要：本页
- 新建实体：[[claude-code]]、[[runoob]]
- 更新实体：[[obsidian]]（主题/插件清单入库）、[[andrej-karpathy]]（二手头衔与日期主张）
- 更新概念：[[llm-wiki]]（实例化变体）、[[llm-wiki-vs-rag]]（复述印证）
- 更新来源页：[[llm-wiki-pattern]]（后续实践回链）
- 更新主题：[[personal-knowledge-management]]（传播期节点 + 页面地图）
- 更新导航：index.md、log.md

## 留给用户的讨论问题

- 目录结构：本库 `raw/` 保持平铺，还是引入教程式 `articles/` `papers/` 子目录？（当前 3 份来源，尚无必要；可随规模再议）
- 教程 15 张截图是否需要下载到 `raw/assets/` 本地留存？（文字层已自足；如需，在 Obsidian 中对本文件按 `Ctrl+Shift+D`）
- 主题与插件：清单里哪些想启用？Dataview / Templater 已在 Backlog；Git 插件与本库「命令行 git」的取舍。
- `output/`（查询结果、lint 报告落盘）是否值得引入？本库现以 `wiki/answers/` 承担「好答案沉淀」，可以吸收 output 的用途。
