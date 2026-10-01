---
title: Memex
type: concept
created: 2026-10-01
updated: 2026-10-01
tags: [knowledge-management, history, hypertext]
status: growing
sources: [raw/as-we-may-think.pdf, raw/llm-wiki.md]
---

# Memex

## 定义

> [[vannevar-bush]] 在《[[as-we-may-think]]》(1945) 中构想的个人知识设备：
> 「a device in which an individual stores all his books, records, and communications, and which is mechanized so that it may be consulted with exceeding speed and flexibility. It is an enlarged intimate supplement to his memory.」

## 为什么重要 / 解决什么问题

- 目标：让个人**全量保有**自己的书、记录与通信并随时调用——对抗「记录堆积远超利用能力」的时代病（Bush 的孟德尔案例）。
- 是 [[personal-knowledge-management]] 与 [[llm-wiki]] 思想的直接前身。Karpathy 的判断：Bush 的构想必网络的实际演化更接近「私人、主动策展、连接与文档同等重要」；**他没解决的是「谁来维护」**——LLM 恰好补上。

## 机制 / 要点（原始设计）

- **形态**：一张书桌——斜面半透明投影屏（可多屏并用）、键盘、成套按钮与拨杆；外观如普通书桌。
- **存储**：微缩胶片（《不列颠百科全书》缩至火柴盒大小）；每天录入 5000 页也需数百年才填满，可以「挥霍地」录入。大部分内容（书籍、图片、期刊、报纸、商业通信）买微缩胶片直接插入。
- **录入**：桌上透明压板 + 干式摄影，手写笔记、照片、备忘录直接拍入胶片；可用触笔做页边批注。
- **调取**：按代码调书（常用代码助记）；拨杆以 1 / 10 / 100 页步进翻阅（左右均可）；特殊按钮直达索引首页；多个投影位可同时驻留不同材料。
- **核心机制**：[[associative-trails|关联索引]]——任意两项可永久相连成路径，可巡游、可分享。「This is the essential feature of the memex.」

## 边界与争议

- **维护问题**：Bush 的设计中，路径的构建与维护劳动完全由用户承担——这正是构想难以落地的要害（对比 [[llm-wiki]] 的分工：人策展、LLM 记账）。
- **技术路线**：以微缩胶片为核心介质；实际历史走了磁记录 → 数字存储的路线。哪些预言成真、哪些落空，可做「预测 vs 实现」对照（见 index Backlog）。
- 与后续超文本（Nelson/Xanadu）、个人 wiki 的传承关系待补。

## 相关页面

- 一手文献：[[as-we-may-think]]；提出者：[[vannevar-bush]]
- 核心机制：[[associative-trails]]
- 思想承接：[[llm-wiki]]、[[llm-wiki-pattern]]、[[personal-knowledge-management]]

## 来源

- raw/as-we-may-think.pdf（主源，第 6-8 节）
- raw/llm-wiki.md（Karpathy 的引述与评价）
