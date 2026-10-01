---
title: "Claude Code + Obsidian 还能这么玩，从零搭一套会自己整理的知识库～"
source: "https://mp.weixin.qq.com/s/ySiAUMffzBDMgsqyMft_PA"
author:
  - "[[RUNOOB]]"
published:
created: 2026-10-01
description:
tags:
  - "clippings"
---
Claude Code / LLM Wiki + Obsidian 这是 Andrej Karpathy（OpenAI 联合创始人）在 2026 年 4 月提出的 LLM Wiki 模式，核心思想是：

```nginx
Obsidian 是 IDE，LLM 是程序员，Wiki 是代码库。
```

我们只负责不断往 Obsidian里面扔东西，文章、PDF、论文、截图、会议记录、ChatGPT 对话…… 剩下的阅读、总结、分类、建立链接、发现冲突、更新旧知识、维护索引，全部交给 Claude Code。

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8Wn1oBmPImsYkmjhpclMMxAEL5okA1YA9xA05FDchTIyFjmEOTkaUhJQ1sQH6fMia0nrCaWib8ln6EPhOibzw4PpzzLoib76Bwf5TY/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

传统 RAG 是每次提问都从原始文件重新检索拼凑答案，LLM Wiki 则是让 AI 一次性编译并持续维护一个结构化的、互相链接的 Markdown 知识库，知识会复利增长，而不是每次从零开始。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/EYxI5IfBe8Xl7jj95M2ymvFk7ibhE1VnRtCMC8SOg0VoNRUy8xZeiczVtFd9NdQZ3stwjNarYRYIz7o7rC3nECbsejmdEY61Qxfia2XdMCK4Hk/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

---

安装使用

先装两个免费工具：

- Obsidian下载地址：https://obsidian.md/zh/
- Claude Code 安装说明：https://code.claude.com/docs/en/quickstart

再推荐装一个 Obsidian Web Clipper 浏览器扩展https://obsidian.md/zh/clipper。

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8WAxv1RMeDzTnIlaEPWRXO6YezE6nNdswuia8mNsJTBFlpuyypwZupgF00exgJgACWmRNhdGKg4SnNqAfRIPjiaxYgPB7mKcfzDM/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

Obsidian Web Clipper 可以一键把网页转成 Markdown 存进 raw/。

创建 Vault 新建一个文件夹作为 Obsidian Vault：

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8Xz5PicI7dsZIwia6hpwpibtfOBod6hzJ8kYaMoeNfu1tjWvS40DaBhUsIXmticPG23F4hL7MTR0IGeibnDeHicEC4ynMDrOcWuL29PM/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=3)

在 Vault 目录打开终端，跑 claude 启动一个会话，把 Karpathy 的完整 gist 贴进去，再说一句类似这样的话：

```objectivec
这是 Andrej Karpathy 的 LLM Wiki 模式：https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f。请把它实现成我的个人知识库： 创建完整的目录结构、CLAUDE.md、index.md、log.md 和模板文件， 并把这份 gist 本身当作第一份要摄入的资料。
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8VhgmoiaUhcmDkyjOXVic7N6klTicC6n8icGfSia0Sym8ySHWgE8ibB9tQNFXiaELvfQ8Svia2c2Zc01oTT6NicLcqOXm4V2ocNx8h4GLew/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=4)

AI 建完后，你应该能在 Obsidian 里看到完整目录树和三个根文件。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/EYxI5IfBe8WeTe9ZibBUtqb1shw46MC61kTNaL1bErMVPpxgnlHuuy4Ok1R9MTvPcy0Gibem6KRgpGyMk2BfRB8tXWT1bZ7CibydmpxtfmCibeM/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=5)
- CLAUDE.md 定义了 ingest/query/lint 的工作流约定，是你和 AI 的共同契约，后面随时可以改。
- index.md 第一行应该已经是 gist 自己的摘要。
- log.md 里应该有第一条 ingest 记录。

三个都齐，初始化就成了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8X46OtgemMMgavicMdMt7tYCJZUMB7icic9Rfia1FNDoJX2znibUDB7zAVq5ujm32Q0VZYUpvLZY8HrUGhp0bDxoPOoic62Pw1q6CBF0/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=6)

目录结构说明：

```perl
my-second-brain/├── CLAUDE.md          # 规则文件，整个系统的宪法├── index.md           # 全库目录├── log.md             # 时间线日志├── raw/               # 原始资料，只进不改│   ├── articles/│   ├── papers/│   └── assets/        # 图片附件├── wiki/              # AI 维护的知识层│   ├── entities/      # 实体页：人物、产品、公司│   ├── concepts/      # 概念页│   ├── sources/       # 每份资料的摘要页│   └── synthesis/     # 跨资料的综合页└── output/            # 查询结果、lint 报告（可选）
```

接着用 Web Clipper 把一篇网页文章存进 `raw/articles/`

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8XlM4WJrVUBf1qsWfBghrEg86tOb1PibDjUMn6Y9ialpExQic13qqZzfFicGAThbYHKka8a8tjKo4oKgaqR8mrXeXs7yic8cYM9drxE/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=7)

可以看到 `raw/articles/ 中我们收集的文章：`

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8Vvceh7UTbdKNCSlqLicx2JZibjeRoqsibWiaYHlan8Qxtg8hH0DGFSRot3jBjibY6NgPwia6jSFibAHSVJTpLBMmQCzVznR3W92l2N64/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=8)

回终端输入命令：

```kotlin
ingest this
```

然后看它干活：读原文 → 和你讨论要点 → 在 `wiki/sources/` 写摘要页 → 更新相关实体页和概念页 → 补交叉链接 → 更新 index.md → 在 log.md 记一笔。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/EYxI5IfBe8U9FVdaic1Cc2icZTicHSlH4WSdkUTatzHmVRgOWd5HsVFkOKFAaMicgouf8wMebnvEFZNCQvWy6u33xpL6DkF9yjjCjSDKXASH79k/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=9)

---

## 核心三层架构

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/EYxI5IfBe8WJPUnKhCbNNbyia94iaC16VOBqxvdVclcwIcXTjsIjXOzJn31TKnTuxcIC8ibnUG6ribHkXg8OQWW8jcnROK0gFBlh8VyyaOWhd48/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=11)
- ## Raw sources（原始层）： 不可变，我们只往里面丢资料（文章、PDF、转录、截图、笔记等），AI 只读不改。
- ## Wiki（知识层）：AI 来维护，写摘要页、实体页、概念页、综合页，自动做交叉链接（\[\[wikilink\]\]），标记矛盾、更新索引，我们只浏览、提问、指导方向。
- ## Schema（规则层）：通常是根目录的 CLAUDE.md（Claude Code 会自动读取）。定义结构、约定、工作流。你和 AI 共同演化这个文件。

## 辅助文件：

- ## index.md：内容目录（每页一行摘要 + 链接），AI 查询时先读
- ## log.md：时间线日志（ingest / query / lint 记录）。

## 三大操作循环：

- Ingest：把新资料丢进 raw/，告诉 AI “ingest this”，AI 读完整源、写摘要、更新相关页面、补链接、记日志。一篇文章可能触碰 10-15 个页面。
- Query：直接问问题，AI 先读 index，再钻进相关页，给出带引用的答案。好答案可以存回 wiki 成为新页面。
- Lint：定期健康检查，找矛盾、过时声明、孤立页、缺失交叉引用、数据缺口。AI 还会建议新问题和新资料。

---

Obsidian 主题 & 插件

接下来分享一些常用的主题与插件。

主题在设置->外观->主题管理搜索与安装：

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8XfiaJiaesfUTibx019aJz7F03lNXd8BQ2GND62sUbNMeibrpWZmjfmfUFl2FYxCCI7KYWSBajRSph9J0nVl5TVpKEhYzibEtZjUTdU/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=13)

插件在设置->第三方插件->社区插件中安装：

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8U5u7QicInlqClblkb99GagQkJ4mG6CMYnlwNY0UddWtI7mjC0FzTGYqsvPo9hDh8xmf4bHiag25atQcgg1ibwHmFiccRCS0Uocd6E/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=14)

一、主题

1、Minimal：极简干净，高度可定制

链接：https://github.com/kepano/obsidian-minimal

社区搜索： Minimal

2、AnuPpuccin：柔和 pastel 配色，暗色模式护眼

链接：https://github.com/AnubisNekhet/AnuPpuccin

3、Blue Topaz：功能丰富，蓝调风格，中文社区热门

链接：https://github.com/PKM-er/Blue-Topaz\_Obsidian-css

4、Things：模仿 Things 3 清爽风格

社区搜索：Things

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8UTRN8s7ibsNQmckoxqSxcsp4n3DY5lO2CSe6NrL9HgT1zZl3XW9oI57Sj7ic8WSoIaicn7QhHcZXEdCVnDeF0G1a0O3qMibNBm0MY/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=15)

5、Sanctum：温暖色调，适合长时间阅读写作

社区搜索：Sanctum

二、插件（Plugins）

1、Excalidraw：手绘草图 / 思维导图

社区搜索：Excalidraw

![Image](https://mmbiz.qpic.cn/mmbiz_png/EYxI5IfBe8Vf2hAOSibibOS294xNqWx88uPyCh4rUNiciap4paBau1DuQBvWbMwJ2k3q3L6RKc44pqkrUwG0jsLxV7wP0mpJ0aSgcvWnYL8hWeg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=16)

2、Templater：动态模板引擎

社区搜索：Templater

链接：https://github.com/SilentVoid13/Templater

3、Dataview：把笔记变成数据库

社区搜索：Dataview

链接：https://github.com/blacksmithgu/obsidian-dataview

4、Tasks：跨笔记任务管理

社区搜索：Tasks

5、Advanced Tables：表格编辑增强

社区搜索：Advanced Tables

6\. Notebook Navigator：三栏文件浏览器 + 日历

社区搜索：Notebook Navigator

7、Calendar：日历视图打开每日笔记

社区搜索：Calendar

8、Kanban：Markdown 看板

社区搜索：Kanban

9、Git：Vault 自动备份到 Git

社区搜索：Git

链接：https://github.com/Vinzent03/obsidian-git

10\. Style Settings：主题颜色 / 字体自定义

社区搜索：Style Settings

11、Iconize — 给文件夹 / 笔记加图标

社区搜索：Iconize