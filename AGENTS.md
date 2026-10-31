# AGENTS.md — 个人知识库 Schema（LLM Wiki 实例）

> 本目录是一个 **LLM Wiki**：由 LLM 增量构建并维护的持久化知识库，位于用户与原始资料之间。模式原始定义见 `raw/llm-wiki.md` 与 [[llm-wiki]]。
> **本文件是三层架构中的「Schema 层」**：规定目录结构、页面约定与工作流，使 Codex 成为有纪律的 wiki 维护者，而非普通聊天机器人。本文件由用户与 LLM 共同演进；每次修改后在文末「Schema 演进记录」追加一条。

## 0. 角色与总原则

- 维护者：在 Codex 会话中，Codex 负责本 wiki 的摘要、交叉引用、归档和记账；用户极少亲手写页面。Claude Code 会话仍可依据 `CLAUDE.md` 维护本库。
- 用户负责：策划资料来源、提出好问题、决定方向与重点、在 Obsidian 中阅读与验证。
- 核心原则：**知识编译一次、持续保鲜**（compile once, keep current），而不是每次查询重新推导。详见 [[llm-wiki-vs-rag]]。
- 实践形态：LLM agent 与 Obsidian 分屏——「Obsidian 是 IDE；LLM 是程序员；wiki 是代码库」。

## 1. 目录结构（三层架构）

```
LLMWiki/
├── AGENTS.md            # Schema 层：本文件
├── CLAUDE.md            # Claude Code 使用的原有 Schema 文件
├── index.md             # 内容目录：所有页面的清单（每次 ingest 后更新）
├── log.md               # 时间线：追加式记录 ingest / query / lint
├── raw/                 # 【原始资料层】只读，永不修改，source of truth
│   ├── assets/          # 图片等附件（Obsidian 附件目录已指向此处）
│   ├── golang-libs-inbox.md # Go 第三方库收件箱（用户每行填一个库名）
│   ├── rust-libs-inbox.md   # Rust 第三方库收件箱
│   ├── jvm-libs-inbox.md    # JVM（Java / Kotlin）第三方库收件箱
│   └── llm-wiki.md      # 第一份资料：Karpathy 的 LLM Wiki gist
├── wiki/                # 【wiki 层】由当前 agent 创建与维护
│   ├── sources/         # 每份资料一个摘要页
│   ├── entities/        # 人物、组织、工具、项目
│   ├── concepts/        # 概念、方法、模式
│   ├── topics/          # 主题总览（hub / synthesis，随来源积累持续演进）
│   ├── comparisons/     # 对比页
│   └── answers/         # 从查询中归档的优质问答
├── output/              # 【产物区】lint 报告、查询产物（幻灯片/图表等）落盘处；非 wiki 页面
└── templates/           # 页面模板（创建新页面前先读对应模板）
```

## 2. 页面规范

### 2.1 Frontmatter（所有 `wiki/` 下的页面必须有；`output/` 产物与 `raw/` 不适用）

```yaml
---
title: 页面标题（可用中文）
type: source | entity | concept | topic | comparison | answer
created: YYYY-MM-DD
updated: YYYY-MM-DD        # 每次修改页面时更新
tags: []                   # 小写英文标签
status: stub | growing | mature | archived
sources: []                # 派生页面必填：依据的 raw 文件，如 [raw/llm-wiki.md]
# 以下按类型补充：
# source 页: author, source_url, raw_file, format
# entity 页: entity_type: person | organization | tool | project | place | other
---
```

- `status` 生命周期：`stub`（占位，明确 TODO）→ `growing`（持续累积）→ `mature`（稳定）→ `archived`（废弃，须注明原因）。

### 2.2 命名与链接

- 文件名：小写 kebab-case、ASCII、全局唯一，如 `llm-wiki.md`；非 ASCII 字符一律转写（é/è/ê→e、à→a、ç→c、œ→oe、撇号→连字符）（`raw/` 不受此限）。
- 链接统一用 wikilink：`[[llm-wiki]]`；需要中文显示名时 `[[llm-wiki|LLM Wiki 模式]]`。
- 指向尚未创建页面的链接是**允许且有意义**的（待建信号），但必须同时登记到 `index.md` 的 Backlog。
- `index.md` / `log.md` / `AGENTS.md` / `CLAUDE.md` 用普通文本提及（不建 wikilink）。

### 2.3 语言

- 正文用中文；术语、专有名词保留英文（RAG、ingest、frontmatter 等）。
- log 条目的操作词用英文（ingest / query / lint / schema / setup），便于 grep。

## 3. 工作流

### 3.1 Ingest 摄入

1. **资料入 raw/**：用户放入文件，或用户给出 URL 由 Codex 下载到 `raw/`（HTML 文章建议用 Obsidian Web Clipper 剪藏转 markdown；图片放 `raw/assets/`）。PDF 资料：原件照存 `raw/`——**poppler 已装（2026-10-01）：PDF 可直接渲染阅读**；同时用 Python(pypdf) 提取同名 `.txt` 作为快速检索层（`.txt` 仅供定位，**引用与事实以原件为准**）。
2. **通读并讨论**：读完全文，向用户提出关键要点、确认重点与存疑处。默认**一次一份、保持用户参与**；用户明确要求时才批量摄入。
3. **写摘要页**：`wiki/sources/<slug>.md`（依据 `templates/source.md`）。
4. **更新知识网络**：创建 / 更新相关 entity、concept、topic 页（一份资料可能触及 10-15 个页面）；新资料与旧论断矛盾时，**在双方页面都显式标注**（`> [!warning] 矛盾`），不允许静默覆盖或平均化。
5. **更新 index.md**：新页面入目录、更新来源/页面计数、Backlog 增减。
6. **追加 log.md**：`## [YYYY-MM-DD] ingest | <标题>`。

### 3.2 Query 查询

1. **先读 `index.md`** 找候选页面（本库规模内足以替代向量检索；规模变大后再引入 [[qmd]]）。
2. 读相关 wiki 页面；需要时回溯 `raw/` 原文核对。
3. **带引用作答**：wiki 页面用 `[[链接]]`，原文注明 `raw/xxx.md` 的位置（行号或小节）。不确定的事实标注「待验证」，不编造。
4. 输出形式按问题选择：markdown 页 / 对比表 / Marp 幻灯片 / matplotlib 图表 / canvas。
5. **产物落盘**：文件型产物（幻灯片、图表、导出的表格/报告）写入 `output/YYYY-MM-DD-<slug>.<ext>`，对话中引用文件路径；并在 index 的 Outputs 区登记一行、记入 log。
6. **好答案回填**：有价值的分析、对比、发现的联系，归档为 `wiki/answers/<slug>.md`（依据 `templates/answer.md`），并更新 index（Answers 区）与 log（`query` 条目）。探索的成果也应当复利。

### 3.3 Lint 巡检

用户要求时执行（建议每月或每积累若干来源后）：

- [ ] 页面间**矛盾**（新旧论断冲突未标注）
- [ ] **过时**内容（已有更新来源推翻，页面未更新）
- [ ] **孤立页**（无任何入链，考虑补充链接或合并）
- [ ] 被提及但**无独立页面**的重要概念（核对 index 的 Backlog，考虑建页或寻找资料）
- [ ] **缺失的交叉引用**（相关页面之间未互链）
- [ ] 可用网络搜索/新资料补齐的**数据缺口**（向用户建议新问题、新来源）

报告落盘为 `output/YYYY-MM-DD-lint.md`，对话中给出摘要；修复动作完成后追加 log：`## [YYYY-MM-DD] lint | <摘要>`，并在 index 的 Outputs 区登记一行。有长期参考价值的结论可另行回填 `wiki/answers/`。

### 3.4 第三方库收件箱与摄入

- `raw/golang-libs-inbox.md`、`raw/rust-libs-inbox.md`、`raw/jvm-libs-inbox.md` 是用户可编辑的输入页。用户在「待摄入」小节每行填一个库名；JVM 页同时收 Java 与 Kotlin 库。仅列名不触发自动摄入。除非用户明确要求，不改动或清空已填的行；摄入进度记在 wiki、index 与 log 中。
- 用户要求摄入时，先按 §3.1 处理指定库；未指定范围时默认一次一个。若名称有歧义，先查官方项目与生态元数据，无法可靠辨认再请用户确认。优先项目官方 GitHub 仓库、官方文档、包注册表；记录查阅日期、版本或文档对应的版本。把实际使用的资料存入 `raw/`，作为可追溯来源；收件箱名称本身不能充当 API 用法证据。
- 每个库的 wiki 实体页依 `templates/library.md` 写：一句话用途、适用场景、安装或依赖声明、1–3 个最重要的典型用法示例、关键限制与来源。Java 与 Kotlin 示例按库的主要使用语言选取；另一语言只有在确有必要时才补。示例应尽量最小、可运行，并核对官方文档；未实际运行须标明。不要为覆盖 API 而堆积示例。
- 摄入每个 Go、Rust、JVM 库时，同时核实其创建者及当前维护者（个人或组织），区分二者及其具体角色；不能仅凭仓库所属组织、提交记录或包发布者推断作者身份。对身份有可靠官方证据的主体，创建或更新 `wiki/entities/` 作者页（依 `templates/library-author.md`），在库页与作者页双向互链。主动查看其官方主页、项目列表或包注册表，寻找有代表性的其他库；将实际查阅的证据存入 `raw/`。作者页分别列出**本库已摄入的库**和**经官方来源核实、但尚未摄入的其他库**，注明主体的角色、查阅日期及来源；后者只是查询线索，不写成已摄入的库页，也不声称清单完整。多个作者分别建页；同名主体须核实身份后消歧。无法可靠确认时在库页标「作者待验证」，将核实事项列入 `index.md` Backlog，不编造作者页或关联库。
- 依据 §3.1 建来源摘要页并更新 `index.md`、`log.md`；只在有实际关联时补其他 wiki 页面。不同语言的同名库用文件名后缀 `-go`、`-rust`、`-jvm` 消歧。

## 4. 导航文件规范

### index.md（内容目录，content-oriented）

- 每个页面一行：链接 + 一句话摘要；按类型分区：Sources / Concepts / Entities / Topics / Comparisons / Answers / Outputs（output/ 产物，链接指向文件）。
- 另设 **Backlog** 区：待建页面与待补事项。
- 每次 ingest 后必须更新；查询时**先读本文件**。
- 适用规模：约 100 份来源 / 数百页以内。
- **Stats 行格式**：`- 来源：**N** 份 ｜ wiki 页面：**N** ｜ Outputs：**N** ｜ 最近更新：YYYY-MM-DD`。

### log.md（时间线，chronological，append-only）

- 条目格式：`## [YYYY-MM-DD] <操作> | <标题>`，操作 ∈ {ingest, query, lint, schema, setup}。
- 每条含：动了哪些文件、关键决定、待办。
- 只追加，不修改历史条目。可用 `grep "^## \[" log.md | tail -5` 查看最近条目。

## 5. 硬性规则（不可违反）

1. `raw/` 中的来源资料**永不修改**（不美化、不重排）；要批注，写到 wiki 页面里。§3.4 的三个收件箱是用户填写库名的例外，Codex 不擅自改动其条目。
2. 每个 wiki 页面必须有 frontmatter；派生页面的 `sources` 必须能追溯到 `raw/` 中的文件。
3. 每次 ingest / 答案或产物归档 / lint 报告落盘，必须同步更新 `index.md` 与 `log.md`。
4. 不静默删页：废弃内容标 `status: archived` 并说明原因。
5. 矛盾必须显式记录在两处，不允许静默覆盖或折中处理。
6. 不确定的事实标注「待验证」，不编造来源。

## 6. 环境与工具

- 本目录是 **Obsidian vault**（已配置）：
  - 附件目录 = `raw/assets/`（剪藏文章后按 `Ctrl+Shift+D` 把图片下载到本地，供 Codex 单独查看；先读文本，再按需查看图片）。
  - 模板文件夹 = `templates/`；graph view 用于观察 wiki 形态（枢纽页 / 孤立页）。
- 可选工具（当前未启用，规模需要时再上）：[[qmd]]（本地 markdown 混合搜索 + LLM 重排，CLI 与 MCP）；Obsidian Web Clipper（网页 → markdown）；Marp（幻灯片）；Dataview（查询 frontmatter 出动态表）。
- 版本管理：**已启用 git**（2026-10-01，分支 `main`）：`.obsidian/workspace*.json` 已忽略，`.gitattributes` 统一 LF 换行；提交身份为仓库级（`--local`）配置。每次有意义的变更（ingest / lint / schema 修改）完成后提交一次。
- 若 Obsidian 正在运行，直接编辑 `.obsidian/*.json` 的配置可能要重启 Obsidian 才生效。

## 7. Schema 演进记录

- **[2026-10-01]** 初始版本（v1）：三层结构（raw / wiki / schema）；wiki 分 6 类目录；确立 frontmatter 字段、kebab-case 命名、wikilink 约定；定义 ingest / query / lint 三个工作流；index / log 规范；6 个页面模板。实例化自 Karpathy 的 LLM Wiki gist（`raw/llm-wiki.md`）。
- **[2026-10-01]** v1.1：PDF 资料在 `raw/` 中同时保存机器提取的同名 `.txt`（本机无 poppler 时的阅读/检索方案；原件仍为唯一权威）。
- **[2026-10-01]** v1.2：安装 poppler（scoop 26.09.0），PDF 可直接渲染阅读；`.txt` 提取保留为检索层。
- **[2026-10-01]** v1.3：新增 `output/` 产物区并确立落盘约定（lint 报告、查询产物；源自 [[claude-code-obsidian-tutorial]] 摄入时的讨论）；相应更新 §1（结构）、§2.1（frontmatter 适用范围）、§3.2（query 新增「产物落盘」）、§3.3（lint 报告落盘）、§4（index 新增 Outputs 区）、§5 规则 3。
- **[2026-10-01]** v1.4：新增词汇系统——`wiki/vocab/`（type: vocab，每词一页）、`templates/vocab.md`、hub 页 [[english-vocabulary]]、收件箱 `raw/vocab-inbox.md`；§3 新增「3.4 Vocab 词汇编译」工作流；§4 增 vocab 例外与 Stats 行格式（源自 query：用户词汇管理需求）。
- **[2026-10-01]** v1.4.1：词条富化标准升级——「词根/词族」小节扩展为「词源/构词」（词头·词根·词尾拆解、来源与演变、同族/派生、记忆钩），并规定词源细节对照 etymonline 等权威源核实；模板与 §3.4 同步（用户请求：深挖每个词的词源要素）。
- **[2026-10-01]** v1.4.2：词条闪卡格式升级——单行卡 `word:::释义` 改为**多行双向卡**（`??`，背面＝释义＋词源摘要），复习同屏可见词源；模板、hub 约定与 §3.4 同步（用户请求：闪卡显示词源深挖内容）。
- **[2026-10-01]** v1.5：词汇系统支持**多词单位**（短语动词 / 习语）——起因是 inbox 收进 `wore on`、`in sight`，而 §3.4 原只写「每词一页」。规定：文件名连字符 kebab-case、`word` 保留空格原形、lemma 取 headword 而非遇到形式（`wore on` → `wear on`）、pos 标 `phr. v.` / `idiom`、建页前查近形页（`in-sight` vs `insight`）。§3.4 第 2 步同步；hub「结构约定」同步（源自用户收词行为本身，非用户显式请求——如不认可可回退）。
- **[2026-10-01]** v1.6：新增**法语词汇系统**，词汇系统改为**按语言分轨**——`wiki/vocab/` 重构为 `wiki/vocab/en/`（17 条英语词条整体迁移，纯重命名，wikilink 按 basename 解析、未断链）与 `wiki/vocab/fr/`；新增 `templates/vocab-fr.md`、hub 页 [[french-vocabulary]]、收件箱 `raw/vocab-fr-inbox.md`；frontmatter 新增 `lang: en | fr`（英语词条同步补齐）与法语字段 `gender` / `plural`；法语词条深度＝阴阳性 + 复数 + 动词「形态要点」（不定式·组别·助动词·过去分词·现在时六形，不列表格），词源以 CNRTL（TLFi）为准；文件名 ASCII 转写 + 全库唯一消歧（跨语言同名 `-fr` 后缀、同语言近形加词性后缀、避开 Windows 保留名 con/aux/nul）；闪卡按语言分子牌组（英语补 `#flashcards/en`、法语 `#flashcards/fr`；模板不再带 `#flashcards` 标签，以免 SRS 把模板解析成幽灵卡）；§1 / §2.1 / §2.2 / §3.4 / §4 同步；顺带修复 `templates/vocab.md` 的活链占位 `[[other-word]]` → 反引号（v1.4 遗留，曾致 Obsidian 自动建页）（源自用户请求：法语词汇系统与英语同构）。
- **[2026-10-01]** v1.6.1：法语词条新增**「英法交叉核对（受影响的英语词）」**小节（每词条必做）——查明受该法语词影响的英语词：**借入**（英 ← 法：路径、年代、拼写/读音漂移、词义异同）与**共祖**（同源但非法语传入）须分清，反向回借（法 ← 英）可留意；英语词条已收录则双向互链；无网络标「待验证」并入 hub 待回补。同步：`templates/vocab-fr.md`（新小节 + 闪卡背面「英法交叉」行）、§3.4 法语要求、法语 hub「概述」与「结构约定」；[[gouvernement]] 实装（government / govern / governor / governance ← 古法语本词族；cyber- 共祖非借入）（源自用户请求：法语词条须列出受影响的英语词做 cross-check）。
- **[2026-10-01]** v1.7：词汇系统整体迁出至独立库 **LLMLangWiki**（`C:\Users\zhenz\Documents\LLMLangWiki`）——单一维护点，避免双份分叉。迁出：55 词条（en 17 / fr 38）、hub english-vocabulary / french-vocabulary、`templates/vocab.md` / `vocab-fr.md`、`raw/vocab-inbox.md` / `vocab-fr-inbox.md`、测验产物与 SRS 配置（topic / answer 模板与 output/README 为复制副本，本库保留）；本文件 §3.4 移除，§1 / §2.1 / §2.2 / §4 相应回退；`index.md` 与 personal-knowledge-management 页同步。词汇今后只在新库维护；原库历史条目与 git 历史保留不动。
- **[2026-10-21]** v1.8：将本库的 agent 指令文件从 `CLAUDE.md` 改为 Codex 可读取的 `AGENTS.md`；将当前维护者、目录说明及工作流中的指称改为 Codex，保留历史版本记录。
- **[2026-10-21]** v1.8.1：应用户要求恢复原有 `CLAUDE.md`，与 `AGENTS.md` 并存；v1.8 所述「改为」现应理解为新增 Codex 入口，而非移除 Claude Code 入口。
- **[2026-10-31]** v1.9：新增 Go、Rust、JVM 三个第三方库收件箱与按需摄入流程；库页使用紧凑模板，要求官方来源、用途摘要及少量典型示例。收件箱是 `raw/` 只读来源规则的用户输入例外。
- **[2026-10-31]** v1.9.1：三个第三方库收件箱的摄入流程新增作者与维护者核实、作者实体页、库页双向链接及其他已核实库的索引；区分已摄入与仅发现的库，身份不明时标待验证。
