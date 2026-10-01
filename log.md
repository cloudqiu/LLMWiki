# Log — 时间线

> 追加式（append-only）记录：ingest / query / lint / schema / setup。
> 条目格式 `## [YYYY-MM-DD] <操作> | <标题>`；`grep "^## \[" log.md | tail -5` 可看最近 5 条。
> 只追加，不修改历史条目（更正以新条目说明）。

## [2026-10-01] setup | 初始化 LLM Wiki 实例

- 建立目录结构：`raw/`（含 `assets/`）+ `wiki/`（sources / entities / concepts / topics / comparisons / answers）+ `templates/`
- 编写 `CLAUDE.md`（Schema v1）、`index.md`、`log.md`、6 个页面模板（source / entity / concept / topic / comparison / answer）
- Obsidian 配置：附件目录 → `raw/assets/`；模板文件夹 → `templates/`；快捷键 `Ctrl+Shift+D` = 下载当前文件附件
- 决定：raw 保持逐字原文、不做任何改动；log 操作词用英文便于 grep；`Welcome.md`（Obsidian 默认欢迎文件）暂留，可删

## [2026-10-01] ingest | LLM Wiki: A pattern for building personal knowledge bases using LLMs

- 来源：`raw/llm-wiki.md`，下载自 https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f （作者：Andrej Karpathy）
- 新建 9 个页面：
  - sources：[[llm-wiki-pattern]]
  - concepts：[[llm-wiki]]、[[retrieval-augmented-generation]]、[[memex]]
  - entities：[[andrej-karpathy]]、[[obsidian]]、[[qmd]]
  - comparisons：[[llm-wiki-vs-rag]]
  - topics：[[personal-knowledge-management]]
- 更新：`index.md`（全部页面入目录 + Backlog 建立）
- 关键决定：目录按页类型分层（sources/entities/concepts/topics/comparisons/answers）；[[vannevar-bush]] 先以「待建链接」存在，登记于 Backlog，待摄入 Bush 原文
- 待办：摄入 Bush《As We May Think》(1945)；Web Clipper / Marp / Dataview 用法页；评估 `git init`

## [2026-10-01] ingest | As We May Think（Vannevar Bush, 1945）

- 来源：`raw/as-we-may-think.pdf`（MIT 课程镜像 https://web.mit.edu/STS.035/www/PDFs/think.pdf ；原文 The Atlantic Monthly, 1945 年 7 月）；另存机器提取文本 `raw/as-we-may-think.txt`（pypdf 提取，含轻微 OCR 噪声）
- 新建 3 个页面：[[as-we-may-think]]（来源页）、[[vannevar-bush]]（实体——**解决了本库第一个待建链接**）、[[associative-trails]]（概念：关联索引/路径）
- 更新 3 个页面：[[memex]]（stub → growing：桌面形态、微缩胶片、投影屏、路径机制全部补入一手描述）；[[personal-knowledge-management]]（1945 节点细化 + 页面地图扩充 + 新增谱系开放问题）；[[llm-wiki]]（补充 [[associative-trails]] 交叉引用）
- 关键综合：原文证实 Bush 的设计把路径的**构建与维护劳动留给用户自己**——与 [[llm-wiki-pattern]] 中「Bush 没解决谁来做维护，LLM 补上」的判断互证；已在 [[memex]] 与 [[associative-trails]] 两页标注
- 决定：PDF 类资料在 raw/ 保留「原件 + 机器提取 .txt」（本机无 poppler）；同步更新 `CLAUDE.md`（Schema v1.1）
- 待办（建议）：Engelbart《Augmenting Human Intellect》(1962)；超文本谱系（Nelson、Wells）

## [2026-10-01] setup | 清理：删除 Welcome.md

- 删除 Obsidian 默认欢迎文件 `Welcome.md`（setup 时暂留、现已按计划移除）；vault 导航完全由 `index.md` 承担

## [2026-10-01] setup | git 版本管理启用

- 初始化 git 仓库：分支 `main`
- `.gitignore`：忽略 `.obsidian/workspace*.json`（本地 UI 状态）与系统文件；其余 `.obsidian/` 配置（附件目录/模板/快捷键）随仓库入库
- `.gitattributes`：`* text=auto eol=lf` 统一换行（消除 Windows 下的 LF/CRLF 告警）
- 提交身份：仓库级（`--local`）配置；根提交包含首日全部内容（schema、2 份来源、12 个页面）

## [2026-10-01] setup | 安装 poppler（PDF 渲染支持）

- `scoop install poppler`（26.09.0；`pdftoppm`/`pdftotext` 等 12 个工具已建 shim）；注册表验证：`scoop\shims` 在用户 PATH，新进程均可解析
- 注意：**本会话**启动早于安装，Read 工具直接读 PDF 需重启 Claude Code 后生效；重启前变通：PowerShell 调 `pdftoppm -png` 转图后再读（已实测第 1 页）
- 同步更新 `CLAUDE.md`（Schema v1.2）

## [2026-10-01] ingest | Claude Code + Obsidian 还能这么玩（RUNOOB 教程）

- 来源：`raw/ClaudeCode-Obsidian-还能这么玩从零搭一套会自己整理的知识库.md`（微信公众号 RUNOOB；原始链接 https://mp.weixin.qq.com/s/ySiAUMffzBDMgsqyMft_PA ）。首次剪藏因微信反爬仅得空壳文件，同日重剪修复；原文未署发布日期
- 新建 3 页：[[claude-code-obsidian-tutorial]]（来源）、[[claude-code]]（实体）、[[runoob]]（实体，stub）
- 更新 6 页：[[llm-wiki]]（实例化变体）、[[obsidian]]（主题 5 款 + 插件 11 款清单入库）、[[llm-wiki-pattern]]（后续实践回链）、[[llm-wiki-vs-rag]]（复述印证）、[[andrej-karpathy]]（二手头衔/日期主张，已标待验证）、[[personal-knowledge-management]]（传播期节点 + 页面地图）
- 关键综合：本教程是 [[llm-wiki-pattern]] 的中文操作化版本；本库与教程为同一模式的两次独立实例化。教程结构变体（`raw/articles` 子目录、`wiki/synthesis`、`output/`）与本库约定（raw 平铺、六类 wiki 目录）差异已显式记录于来源页——**非矛盾**（gist 明言结构示例性）
- 存疑（待验证）：Karpathy「2026-04 提出」与「OpenAI 联合创始人」（二手）；RUNOOB 与菜鸟教程关系；Claude Code「免费工具」说法
- 待办：① raw 子目录化评估（已入 Backlog）；② 教程 15 张远程截图未下载本地（文字层自足）；③ 主题/插件启用选择（Dataview / Templater 已在 Backlog）
- schema：无变更；index.md 已同步（来源 2→3、页面 12→15）

## [2026-10-01] schema | 采纳 output/ 落盘约定（v1.3）

- 决议（源自 [[claude-code-obsidian-tutorial]] 摄入时的讨论问题）：lint 报告与查询产物**落盘**到新建的 `output/`；`wiki/answers/` 继续承担「有沉淀价值的问答回填」，两者分工写入 schema
- 修改 `CLAUDE.md`（v1.3）：§1 结构（+`output/`）、§2.1（frontmatter 适用范围）、§3.2（query 新增「产物落盘」步）、§3.3（lint 报告落盘至 `output/YYYY-MM-DD-lint.md`）、§4（index 新增 Outputs 区）、§5 规则 3（同步义务扩展到产物）、§7（v1.3 记录）
- 新建 `output/README.md`（约定说明）；`index.md` 增加 Outputs 区、Backlog 调整（raw 子目录化仍待议）；来源页 [[claude-code-obsidian-tutorial]] 讨论问题同步决议
- 待办：raw 子目录化评估仍开放；其余讨论问题（截图下载、主题/插件启用）未决

## [2026-10-01] query | 词汇管理方案设计（英语生词）

- 问题：用户希望用本库管理已收集的英语词汇（散落各处未整理；以「阅读遇到的词」与「工作/专业词汇」为主）
- 方案要点：`raw/vocab-inbox.md` 收词（用户）→ `wiki/vocab/<word>` 逐词编译与富化（LLM，含闪卡行）→ 词族/易混/主题综合 → 复习双轨（SRS 插件排程 + Claude 按需出题）
- 决策（用户选定）：① 复习 = SRS 插件 + Claude 出题；② 无从批量导入，自 inbox 逐步收录；③ 标签以来源（src/）+ 领域（domain/）为主
- 回填：要点落 [[english-vocabulary]]（hub）；schema 变更见下一条
- 插件调研（2026 现状）：Spaced Repetition（经典生态）、LearnKit / EngramQuest（FSRS）、English Vocabulary Learning Plugin / Klomimory（语言学习专用）、Glossa / AI Flashcard Generator（AI 制卡）——选型待定，记于 hub

## [2026-10-01] schema | 词汇系统 v1.4

- 新增：`wiki/vocab/`（新页面类型 vocab，每词一页、不逐条进 index）、`templates/vocab.md`、hub 页 [[english-vocabulary]]、收件箱 `raw/vocab-inbox.md`（用户追加；Claude 只读）
- 修改 `CLAUDE.md`（v1.4）：§1（结构 +vocab/）、§2.1（vocab 页 frontmatter 字段）、§3.4（新增「Vocab 词汇编译」工作流）、§4（vocab 例外 + Stats 行格式）、§7（v1.4 记录）
- 更新：`index.md`（Topics + Stats + Backlog）；[[personal-knowledge-management]]（记忆方法开放问题 → 已启动 + 页面地图）
- 待办：SRS 插件选型与安装；首批词条待用户收词后编译

## [2026-10-01] ingest | vocab: 首批 3 词（deplete / off-kilter / unravel）

- 来源：`raw/vocab-inbox.md`（用户追加）；三词均出自书籍《Mattering》→ 标签 `src/mattering`
- 新建词条 3 个：[[deplete]]、[[off-kilter]]、[[unravel]]（遇到形式 "unraveling" 归并至 lemma）
- 首次执行 §3.4 词汇编译流程；更新 [[english-vocabulary]]（进度 0→3 + 最近入库）、`index.md`（Stats）
- 备注：例句为 LLM 生成；词源细节（kilter 词源不明、ravel 荷兰语来源）已在词条内说明
- 待办：SRS 插件仍未装（见 hub 开放问题）；随积累考虑词族 / 易混综合页

## [2026-10-01] query | vocab 测验 #1（deplete / off-kilter / unravel）

- 首次复习测验：Claude 出题 9 道（填空 3 / 英译中 2 / 中译英 2 / 短语 1 / 辨析 1），对话内作答
- 产物落盘：`output/2026-10-01-vocab-quiz-01.md`（含答案解析与作答记录区）；index.md Outputs 区首条 + Stats（Outputs 0→1）
- 评分结果随后记入产物文件（不改历史条目）

## [2026-10-01] setup | SRS 插件安装（Spaced Repetition v1.15.4）

- 用户完成安装并启用：`.obsidian/plugins/obsidian-spaced-repetition/`；`.obsidian/community-plugins.json` 启用清单已入库
- 配置核对（安装默认值，与词条约定一致）：flashcardTags=`#flashcards`、分隔符 `::` / `:::`；算法 SM-2-OSR（FSRS 可选未切）；dataStore=NOTES（排程将以 `<!--SR:…-->` 注释写回词条笔记）
- `.gitignore` 追加：插件本体（main.js / styles.css）不入库，仅跟踪启用清单与插件 manifest/data（设置）
- hub [[english-vocabulary]]：新增「SRS（复习层，已装）」小节，移除开放问题中的选型项；index Backlog 移除该项
- 待办：首批卡已就绪（3 词条）——可开始首次复习
