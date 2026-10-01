---
title: 英语词汇（Vocabulary）
type: topic
created: 2026-10-01
updated: 2026-10-01
tags: [vocabulary, english, learning]
status: growing
sources: [raw/vocab-inbox.md]
---

# 英语词汇（Vocabulary）

## 概述

本库的英语词汇管理系统（2026-10-01 建立）。分工：

> `raw/vocab-inbox.md` 收词（用户）→ `wiki/vocab/` 逐词编译与富化（LLM）→ 词族 / 易混 / 主题综合（持续）→ 复习双轨：SRS 插件排程 + Claude 按需出题。

词条富化含：IPA、词性、双语释义、例句（含翻译）、词根/词族、同义/搭配、易混提示；不确定信息标「待验证」。阅读词条本身即为第一遍复习；`learning` 字段（new → learning → known）跟踪掌握度。

## 进度

- 词条：**15**（new 15 ｜ learning 0 ｜ known 0）；更新于 2026-10-01
- 待处理：inbox 暂无积压（七批共 15 词已编译，均出自《Mattering》）
- 词条（15）：[[deplete]]、[[off-kilter]]、[[unravel]]、[[turquoise]]、[[flurry]]、[[nook]]、[[counterweight]]、[[disconcert]]、[[hospice]]、[[decor]]、[[unto]]、[[endometriosis]]、[[sew]]、[[competent]]、[[faucet]]
- **待回补（联网后）**：[[unto]]、[[endometriosis]]、[[sew]]、[[competent]]、[[faucet]] 5 词未对照 etymonline / 医学词典（2026-10-01 会话出网被 sinkhole，已逐条标「待验证」）；其余 10 词编译时均已对照核实。**核对债务在累积**——`web_fetch` 对全部域名失败（DNS 解析至保留段 198.18.0.0/15），需恢复出网后才能一次性清账

## 怎么用

1. **收词**：把生词追加到 `raw/vocab-inbox.md`（一行一个，可附来源/例句）；或在会话中口述「这批词：…」——Claude 先**原样**记入 `raw/vocab-capture-YYYY-MM-DD.md` 再编译。
2. **编译**：说「ingest vocab」→ 去重、逐词建/更新词条（每批 20-50 词）、更新本页、记 log。
3. **复习**：已装 SRS（见下节）——每日 `Ctrl+P → "Review Flashcards from all notes"` 刷卡；想测验就说「考我：最近 20 个 new 词」→ Claude 出题（cloze / 翻译 / 辨析），产物落 `output/`（示例：[[2026-10-01-vocab-quiz-01]]）。

## SRS（复习层，已装）

- 插件：**Spaced Repetition v1.15.4**（st3v3nmw；2026-10-01 安装并启用）
- 当前配置（安装默认值，与本库约定一致）：闪卡标签 `#flashcards` ｜ 单行卡 `::`、双向卡 `:::` ｜ 算法 SM-2-OSR（插件设置里可切 **FSRS**）
- 排程数据：`dataStore = NOTES`——复习后插件的排程信息会以 `<!--SR:…-->` 注释写进词条笔记（正常现象，git 中会见到此类小改动）
- 入口：`Ctrl+P` → "Review Flashcards from all notes"；或侧边栏复习队列（启动时自动打开）

## 结构约定

- 词条路径：`wiki/vocab/<word>.md`（小写 lemma；**不逐条进 index.md**）
- 标签：`src/<来源>`（如 src/reading、src/书名-slug，标注在哪读到的）、`domain/<领域>`（如 domain/tech、domain/finance，工作/专业领域）——按需取用
- 闪卡：词条「闪卡」小节内**多行双向卡**（`word` ⏎ `??` ⏎ 释义＋词源摘要的背面），小节标题带 `#flashcards` 标签——插件凭此发现卡片、复习时同屏显示词源；如需按来源分子牌组，可用 `#flashcards/<子牌组>`（如 #flashcards/mattering）
- 发现方式：全库按标签自动发现（卡片集中在 `wiki/vocab`）

## 词族 / 综合页

（暂无已建页面——出现值得综合的词族、易混对或主题簇时在此登记，并链到对应页面）

- **候选（2026-10-01）**：「直到 / 到」虚词簇 **unto · until · till**——三者同出日耳曼语「直到」义（un- ← 哥特语 und），中古英语中 unto 与 until 一度同义；待 until、till 收词后建一页对照（含 unto / onto 拼写易混）。当前已在 [[unto]] 词条内先行记录
- **候选（2026-10-01）**：**希腊医学构词零件**（endo- / metr- / hyster- / -osis / -itis）——由 [[endometriosis]] 触发的可复用零件库：拆得动 endometriosis，就同时拿下 endometritis、adenomyosis、myometrium、hysterectomy 等一串词（含 -osis 病名 vs -itis 炎症的易混）。词条尚未收词，先登记；愿建页就说一声
- **候选（2026-10-01）**：**同音易混簇 sew · sow · so**（均读 /səʊ/，拼写高发错点）——[[sew]] 已收词，sow / so 未收；再遇同音簇可合并建一页拼写辨析（每词条内已先记录）

## 开放问题

- 例句来源：当前为 LLM 生成 + 待验证标记；是否引入词典核对流程？
- Dataview（未装）：装上后本页可改为动态统计表（按 learning / tags 查询）。

## 来源

- raw/vocab-inbox.md（收词入口）
- 系统设计：2026-10-01 query 会话（决策记录见 `log.md`）
