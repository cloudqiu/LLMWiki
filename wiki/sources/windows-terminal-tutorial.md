---
title: "Windows Terminal：把黑框变好看"
type: source
created: 2026-10-06
updated: 2026-10-06
tags: [tutorial, terminal, command-line, windows, ai-tooling]
status: growing
author: 凡哥哥（微信公众号「光影紐扣」，待验证）
source_url: https://mp.weixin.qq.com/s/kR6FJZ-jdRkxIhn9SBbvRw
raw_file: raw/Windows Terminal：把黑框变好看.md
format: article
---

# Windows Terminal：把黑框变好看

## 来源信息

- 作者 / 出处：署名「凡哥哥」，微信公众号「光影紐扣」（→ [[guangying-niukou]]；署名与账号主体的关系**待验证**）
- 发布 / 获取日期：原文署 Oct 4, 2026；2026-10-06 剪藏入库（Obsidian Web Clipper，frontmatter 为剪藏器所加）
- 本地文件：`raw/Windows Terminal：把黑框变好看.md`
- 原始链接：https://mp.weixin.qq.com/s/kR6FJZ-jdRkxIhn9SBbvRw
- 形式：面向非技术读者的科普短文——口语化、比喻驱动、附「命令卡片」表格（含危险等级标注）
- 图片：无（纯文字层）

## 一句话概括

> 一篇写给「电脑上有三个黑框」的人的入门科普：[[windows-terminal]] 不替代 [[command-prompt|CMD]]、[[powershell]]、[[wsl]]，只是给它们加一个统一外壳——**「不是新命令，是新窗口」**，因此它是 AI 时代跑命令的「统一入口」。

## 核心要点

- **终端 ≠ shell**（本文真正的概念贡献）：CMD / PowerShell / WSL 是三个各自独立的 shell 环境，Windows Terminal 只是承载它们的**窗口**；换壳不改变命令语义（原文 L38、L162、L168）。
- **统一入口的价值**：一个窗口容纳三种环境，靠标签页切换 + 分屏同屏对照，解决「三个窗口堆任务栏、切来切去」的痛点（原文 L22-24、L114-124）。
- **AI 场景下的三条实用理由**：① AI 给的命令可能来自三个世界，切标签即可跑；② 复制粘贴改为标准快捷键；③ 分屏对照教程与执行，减少「跑错环境」（原文 L110-140）。
- **外观即门槛**：「好看，心情好」不是玩笑——清晰现代的终端降低心理门槛，让人不再觉得命令行是「黑客才用的东西」（原文 L142-146）。
- **落地建议**：把默认终端应用改为 Windows Terminal（原文 L178-187）。
- **避坑三条**：换壳不改变命令；先看标签页名字再粘贴；别一上来就折腾 JSON 配置（原文 L164-176）。

## 关键细节（值得引用的原文片段）

<!-- 引用时注明在 raw 文件中的大致位置（行号或小节名） -->

- L36：「Windows Terminal 是一个现代化的终端工具，能把 CMD、PowerShell、WSL 装进同一个窗口。」
- L38：「它不是替代它们。CMD 还是 CMD，PowerShell 还是 PowerShell，WSL 还是 WSL。Windows Terminal 只是给它们换了一个好看的『外壳』，让你在一个窗口里就能切换。」
- L40-46（核心比喻）：「CMD、PowerShell、WSL 是三间房子。以前你每次只能进一间，出来再进另一间。Windows Terminal 是一条走廊，三间房子都开在走廊上，你走几步就能换一间。」
- L118-120（三世界命令举例）：`cmd: dir / ipconfig / .bat` ｜ `powershell: Get-Process` ｜ `wsl: curl / apt / python / ollama`。
- L144-146：「命令行本来就容易让人紧张。一个清晰、好看的终端，能降低心理门槛。你不再觉得『这是黑客才用的东西』，而是『这是我电脑上的一个正常工具』。」
- L162：「Windows Terminal 不是新命令，是新窗口。」
- L168：「别以为换了个好看的终端，命令就能通用了。」
- L193：「明天我们进入第三周：Python 篇。」（→ 本系列是连载教程，见 [[ai-era-command-line]]）

## 与既有知识的关系

- **新领域（本库首份非 PKM 来源）**：现有 3 份来源都在「LLM Wiki / 知识管理」线上；本篇是**操作系统与开发环境层**的内容。二者并非无关——本库的维护者 [[claude-code]] 就运行在终端里，Windows Terminal 是它的宿主外壳之一（见 [[claude-code]] 页新增链接）；但**库的主题边界是否随之扩张，需用户定夺**（见下方讨论问题）。
- **支持 / 印证**：与 [[claude-code-obsidian-tutorial]] 属同一现象——中文公众号正在成体系地做「AI 工具入门」教学（该篇讲知识库，本篇讲命令行）。两者共同构成「非技术用户如何搭起本地 AI 环境」的连续叙事。
- **矛盾 / 修正**（与微软官方文档对不上，非与其他来源冲突）：
  - **分屏快捷键的方向**：原文记 `Alt + Shift + +` 为「分屏（上下）」。按微软当前默认键位，`alt+shift+plus` 是**向右**复制窗格（左右并排），向下的那个是 `alt+shift+-`；`alt+shift+d` 则是 `DuplicatePaneAuto`（方向随当前窗格自动）。→ 已在 [[windows-terminal]] 以 callout 标注，原文按「待验证」处理。
  - **`Ctrl + C` 的前提**：原文表格将复制列为 🟢 绿色。实际上仅**在有选中内容时** `Ctrl+C` 才是复制，否则它仍是中断信号（SIGINT），把正在跑的命令打断——对新手而言这正是最需要提醒的一条，原文未提。
- **存疑 / 待验证**：
  - 「Windows 11 已经自带 Windows Terminal」——**已验证**：Win11 22H2 起 Windows Terminal 成为默认命令行体验（需 WT ≥ 1.15，随 KB5019509 起）。
  - 「设置 → 启动 → 默认终端应用程序」的路径**已验证**（与官方一致）。
  - `winget install Microsoft.WindowsTerminal` 的包 ID **待验证**：官方文档写法为 `winget install --id Microsoft.WindowsTerminal -e`。
  - `Ctrl + V` 直接粘贴**待验证**：旧版默认是 `Ctrl + Shift + V`，较新版本才把 `Ctrl + V` 收入默认键位，具体版本未核。
  - 作者「凡哥哥」与公众号「光影紐扣」的对应关系**待验证**（剪藏器 frontmatter 写 `author: 凡哥哥`，正文署「凡哥哥 光影紐扣」）。

## 由本来源派生 / 更新的页面

- 来源摘要：本页
- 新建实体：[[windows-terminal]]、[[command-prompt]]、[[powershell]]、[[wsl]]、[[winget]]、[[guangying-niukou]]
- 新建概念：[[command-line-interface]]（终端 vs shell 的区分）
- 新建主题：[[ai-era-command-line]]（本连载的 hub）
- 更新实体：[[claude-code]]（补「运行于终端」的宿主外壳链接）
- 更新导航：index.md、log.md

## 留给用户的讨论问题

- **主题边界**：本库此前是纯 PKM / LLM Wiki 库，本篇把它扩到了「Windows 开发环境」。这是否是本库的意图？
  - 若是 → 后续同类文章（预告的 Python 篇、WSL 篇等）按 [[ai-era-command-line]] hub 归集即可。
  - 若不是 → 建议另开一库（如同词汇系统迁往 LLMLangWiki 的处理），本页可整体迁移。
  - *2026-10-06：用户未要求迁出 → **页面留存、维持现状**。触发条件若再现（同类来源持续涌入、与 PKM 线争夺库的重心）再议。*
- **连续性** — *已决议（2026-10-06）：**不回补***。该连载前几周文章不入库；[[ai-era-command-line]] 的脉络以本篇为起点，前史留白。
- **实用动作** — *已决议（2026-10-06）：**不做***。不调整本机默认终端与外观配置（[[windows-terminal]] 的 settings.json 美化仍留在 backlog，需要时再取）。
