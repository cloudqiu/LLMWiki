---
title: 法语词汇（Vocabulaire）
type: topic
created: 2026-10-01
updated: 2026-10-01
tags: [vocabulary, french, learning]
status: growing
sources: [raw/vocab-fr-inbox.md]
---

# 法语词汇（Vocabulaire）

## 概述

本库的**法语**词汇管理系统（2026-10-01 建立），与英语系统 [[english-vocabulary]] 同构分轨、独立收词与计数：

> `raw/vocab-fr-inbox.md` 收词（用户）→ `wiki/vocab/fr/` 逐词编译与富化（LLM）→ 词族 / 易混 / 主题综合（持续）→ 复习双轨：SRS 子牌组 `#flashcards/fr` + Claude 按需出题。

词条富化含：IPA、词性、**阴阳性与复数**、**形态要点**（动词：不定式·组别·助动词·过去分词·现在时六形，不列表格）、双语释义、例句（含翻译）、词源/构词（对照 **CNRTL（TLFi）** 核实）、同义/搭配/易混（含 faux amis）；不确定信息标「待验证」；`learning` 字段（new → learning → known）跟踪掌握度。

## 进度

- 词条：**0**（new 0 ｜ learning 0 ｜ known 0）；更新于 2026-10-01
- 待处理：inbox 暂无积压（等待首批收词）
- **待回补（联网后）**：暂无——首批词条编译起累积（法语词源一律以 CNRTL/TLFi 为准；出网被 sinkhole 期间一律标「待验证」）

## 怎么用

1. **收词**：追加到 `raw/vocab-fr-inbox.md`（一行一个，可附来源/例句；**重音、撇号照写**）；或会话口述——Claude 先**原样**记入 `raw/vocab-fr-capture-YYYY-MM-DD.md` 再编译。
2. **编译**：说「**ingest vocab-fr**」→ 去重、逐词建/更新词条（每批 20-50 词）、更新本页、记 log（`ingest | vocab-fr: …`）。
3. **复习**：SRS 刷卡（法语卡在 `flashcards/fr` 子牌组，可只复习法语）；想测验就说「考我：最近 20 个法语 new 词」→ Claude 出题，产物落 `output/`。

## SRS（复习层，与英语共用插件）

- 插件：Spaced Repetition v1.15.4（同一实例、同一配置：闪卡标签 `#flashcards`，**子标签自动纳入**）
- 法语卡：小节标题 `## 闪卡 #flashcards/fr` → 归入 **flashcards/fr 子牌组**（英语为 `flashcards/en`；复习「全部」时两语混合，牌组树里选 fr 可隔离）
- 排程数据：`dataStore = NOTES`——排程信息以 `<!--SR:…-->` 注释写进词条笔记
- 入口：`Ctrl+P` → "Review Flashcards from all notes"

## 结构约定

- 词条路径：`wiki/vocab/fr/<word>.md`（小写 lemma；**不逐条进 index.md**）
- **lemma 规则**：动词→不定式（遇到 `suis` 归并到 `être`）；名词→单数、不带冠词（阴阳性进 `gender` 字段）；形容词→阳性单数；代词式动词带 se（`se laver` → `se-laver.md`）；多词表达取词典 headword
- **文件名一律 ASCII 转写**（重音只留在 `word` 与正文/卡片里）：

  | 法语字符 | 转写 | 例 |
  | --- | --- | --- |
  | é è ê ë | e | école → `ecole.md` |
  | à â | a | là → `la.md`（与 `la` 撞名 → 消歧） |
  | î ï | i | île → `ile.md` |
  | ô | o | tôt → `tot.md` |
  | ù û | u | où → `ou.md`（与 `ou` 撞名 → 消歧） |
  | ç | c | français → `francais.md` |
  | œ æ | oe / ae | cœur → `coeur.md` |
  | 撇号 ' ’ | - | l'air → `l-air.md`；aujourd'hui → `aujourd-hui.md` |
  | 连字符 | 保留 | peut-être → `peut-etre.md` |
  | 空格（多词单位） | - | avoir l'air → `avoir-l-air.md` |

  理由：Obsidian 按 basename 解析链接，而 é / œ 存在 NFC/NFD 两种编码——ASCII 化杜绝重影页面。

- **命名消歧**（basename 必须**全库唯一**；建页前先扫全库，含 `templates/`——`concept.md`、`source.md` 等本身就是法语词）：
  - 跨语言同名（décor / decor、hospice、turquoise、compétent / competent）：法语页加 `-fr`（`decor-fr.md`），两页互链
  - 同语言近形（ou / où、a / à、la / là、sur / sûr、du / dû、cote / côte / coté）：**一律先用带词性后缀的名字**（`ou-conj.md` / `ou-adv.md`），避免「先到先得」的任意性，并登记下表
  - **Windows 保留名**（con / prn / aux / nul / com1-9 / lpt1-9）加后缀（`con-adj.md`、`aux-prep.md`）
- 标签：`src/<来源>`、`domain/<领域>`；语言由 frontmatter `lang: fr` 标记
- 闪卡：`## 闪卡 #flashcards/fr` 内**多行双向卡**；正面＝词（照写重音），背面＝释义＋形态＋词源摘要；阴阳性 / 变位可加挖空卡（`==…==`）。**单独成行的 `?` / `??` 是插件分隔符**，正文避免
- 发现方式：全库按标签自动发现（卡片集中在 `wiki/vocab/fr`）

## 命名消歧登记表

| 页面 | 原形 | 说明 |
| --- | --- | --- |
| （空——触发消歧时在此登记） | | |

## 词族 / 综合页

（暂无——出现 faux amis 簇、同音簇、构词零件（-tion / -ment / re- / dé-）或英法同源对（décor ↔ [[decor]]）等值得综合的内容时在此登记）

## 开放问题

- 例句来源：当前为 LLM 生成 + 待验证标记；是否引入 CNRTL / Le Robert 核对流程？
- 「形态要点」是否提升为 frontmatter 字段（便于日后 Dataview 查询）？
- 英语系统的 etymonline 待回补（7 条）与本系统 CNRTL 待回补，联网后一并清账。

## 来源

- raw/vocab-fr-inbox.md（收词入口）
- 系统设计：2026-10-01 会话，schema v1.6（决策记录见 `log.md`）
