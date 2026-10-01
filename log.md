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

## [2026-10-01] query | 词源深挖：deplete / off-kilter / unravel（etymonline 核对）

- 请求：为现有词条补全词源深挖（词头 / 词根 / 词尾要素、来源与演变）
- 词源要点：**deplete**＝1807 年由 depletion 反向构词（拉丁 dēplēre「倒空」，PIE \*pele-「填满」的家族里唯一的「倒空」）；**unravel**＝un-²（反向前缀）+ 荷兰语 ravelen，c.1600，附带「ravel 同义又反义」悖论；**off-kilter**＝kilter 词源不明（方言 kelter c.1600），out of kilter 首见 1620s，off- 为「偏离常规」组合成分
- 落地：3 个词条「词根/词族」→「词源/构词」升级（含拆解/演变/同族/记忆钩）；`templates/vocab.md` 与 CLAUDE.md §3.4 同步（v1.4.1）
- 核对依据：etymonline（deplete / unravel / ravel / kilter 四页）；日期与词形均采用其记载，不作推测
- 备注：data.json 显示算法仍为 SM-2-OSR（FSRS 切换待用户在插件设置中完成）

## [2026-10-01] query | 闪卡显示词源：卡格式升级为多行双向卡（??）

- 需求：复习卡片时同屏显示词源深挖内容
- 机制核对（官方文档 stephenmwangi.com）：多行卡 `?` / 双向 `??`，两侧可多行、须「贴合」分隔行；卡片只渲染卡内文本，不自动带出页面其它段落——故将词源摘要写入卡背
- 变更：3 个词条闪卡改为多行双向卡（背面＝释义＋词源摘要＋同族/联想）；templates/vocab.md、CLAUDE.md §3.4 与 §7（v1.4.2）、hub 结构约定同步
- 备注：旧卡无复习历史（scheduleData 为空），重构无损失；如需主动测验词源可另加挖空卡（`==…==`），暂不默认

## [2026-10-01] ingest | vocab: 第二批 3 词（turquoise / flurry / nook）

- 来源：`raw/vocab-inbox.md`；均出自《Mattering》→ `src/mattering`；去重跳过已编译的 3 词（deplete / off-kilter / unravel）
- 新建词条 3 个：[[turquoise]]、[[flurry]]、[[nook]]——按 v1.4.1 标准（词源对照 etymonline）+ v1.4.2 卡格式（多行双向卡，卡背含词源）
- 词源要点：**turquoise**＝法语「土耳其石」（取道土耳其传入欧洲，实产波斯）；**flurry**＝1690s「一阵疾风」，来源不确定（疑拟声）；**nook**＝c.1300「角落」，来源不明（或古诺斯语 nokke）
- 更新：[[english-vocabulary]]（进度 3→6，词条列表全列）、`index.md`（Stats）
- 待办：无积压；SRS 已装、可开始首刷（词条已达 6 个，够刷一轮）

## [2026-10-01] ingest | vocab: 第三批 2 词（counterweight / disconcert）

- 来源：`raw/vocab-inbox.md`（《Mattering》）→ src/mattering；去重跳过 6 词
- 新建词条 2 个：[[counterweight]]、[[disconcert]]（遇到形式 disconcerting 归并至 lemma）
- 词源要点：**counterweight**＝透明复合词（counter- ← 拉丁 contra；weight ← 古英语 / PIE \*wegh-）；**disconcert**＝1680s，法语 disconcerter ← 意大利 concertare「使协调」，dis- 反转之；同根 \*krei- 家族（certain / discern / crisis）
- 备注：etymonline 与 Wiktionary 均无 counterweight 成词年代——已按 schema 标「待验证」而非编造
- 更新：[[english-vocabulary]]（6→8）、`index.md`（Stats）

## [2026-10-01] ingest | vocab: 第四批 2 词（hospice / decor）

- 来源：`raw/vocab-inbox.md`（《Mattering》）→ src/mattering；去重跳过 8 词
- 新建词条 2 个：[[hospice]]、[[decor]]
- 词源要点：**hospice**＝1818「旅人招待所」→1879「临终机构」；拉丁 hospes（客人/主人），与 hospital / hotel / hostile 同出 PIE \*ghos-ti-「陌生人」家族；**decor**＝1897（原为剧场用语），法语 décor 逆构自 décorer ← 拉丁 decorare，英语恰好还原了拉丁名词 decor 本身；同根 \*dek-（decent / dignity / doctor / orthodox）
- 更新：[[english-vocabulary]]（8→10）、`index.md`（Stats）
- 备注：hospice 词条未采纳「运动始于 1960s 英国」作例句（无本批来源支撑），改用中性例句

## [2026-10-01] ingest | vocab: 第五批 1 词（unto）

- 来源：`raw/vocab-inbox.md`（《Mattering》）→ src/mattering；去重跳过 10 词（`unraveling` 归并至 lemma [[unravel]]）
- 新建词条 1 个：[[unto]]（本批 inbox 仅新增 1 词，git diff 已确认）
- 词源要点：**unto**＝「直到、及于」义的日耳曼语前缀（哥特语 und / 古诺斯语 unz / 古高地德语 unz）＋ 古英语 tō「到」，约 1300 年入英语；与 until / till 同族（中古英语中 unto 与 until 一度同义），早期现代英语兼作 to 的「与格」形式（KJV：spake unto Moses），19 世纪后退入文学/法律/宗教语体
- 易混提示：unto / to / until / onto（unto↔onto 仅差一字母）
- **备注（环境限制）**：本会话出网被整体 sinkhole（所有域名解析至保留段 198.18.0.0/15，`web_fetch` 全线失败），etymonline / Wiktionary **无法访问**——词源按既有知识撰写，「成词机制（un-+to 复合 vs. until 类推）」与「印欧语更早来源」已标**待验证**；恢复联网后应回补 etymonline 核对（词条与 hub 均已记该待办）
- 更新：[[english-vocabulary]]（进度 10→11、新增待回补项、词族候选 unto/until/till）、`index.md`（Stats：vocab 10→11）

## [2026-10-01] ingest | vocab: 第六批 1 词（endometriosis）

- 来源：`raw/vocab-inbox.md`（《Mattering》）→ src/mattering；去重跳过 11 词
- 新建词条 1 个：[[endometriosis]]（首个非通用语域词条；新增 `domain/medical` 标签，为该词条判断——若与 hub 的「工作/专业领域」约定不符可撤）
- 词源要点：**endometriosis**＝endometrium（19 世纪解剖学术语：endo- 希腊「在内」+ metr- 希腊 mētra「子宫」+ -ium）再挂希腊病理后缀 -osis；字面「内膜的病变状态」；一般追溯到 John A. Sampson（1927）命名——**待验证**（无网络）
- 易混要点：endometritis（-itis 炎症，一字之差）、adenomyosis（内膜进肌层）、endometrium（正常内膜）；同族 metr- 与 hyster- 两套「子宫」词根
- **备注（环境限制）**：出网仍被 sinkhole（198.18.0.0/15），etymonline / 医学词典不可达；「1927 年 Sampson 造词」标待验证，与 [[unto]] 一并留待联网回补
- **顺带发现的仓库杂物**：根目录出现空文件 `other-word.md`（2026-10-01 12:47 生成）——成因是 `templates/vocab.md` 里作占位示例的 wikilink `[[other-word]]` 被点击后由 Obsidian 自动建note。未删除（schema 规则 4：不静默删页），待用户定夺；建议把模板与 hub 中的该占位改为反引号 `other-word` 以免再生
- 更新：[[english-vocabulary]]（进度 11→12、待回补项并入本词、新增「希腊医学构词零件」词族候选）、`index.md`（Stats：vocab 11→12）

## [2026-10-01] ingest | vocab: 第七批 3 词（sew / competent / faucet）

- 来源：`raw/vocab-inbox.md`（《Mattering》）→ src/mattering；去重跳过 12 词
- 新建词条 3 个：[[sew]]、[[competent]]、[[faucet]]
- 词源要点：**sew**＝古英语 siwian ← 原始日耳曼语 \*siwjanan ← PIE \*syu-「缝、绑」，同族 seam / suture / couture，本族词故拼写与变化不规则；**competent**＝拉丁 com-「共同」+ petere「追求」→ competere「共同争取、相合」→「够得上标准」，与 compete/competition 同根，同族 petition / appetite / impetus / repeat（PIE \*pet-），另有法律义「有管辖权的、有行为能力的」（competent authority）；**faucet**＝古法语 fausset「塞子、龙头」← fausser「弄坏」← 拉丁 falsus「假的」（false/fail/fault 家族），约 1400 年入英语，原指酒桶取酒塞嘴
- 易混要点：**sew / sow / so 三词同音 /səʊ/**（拼写高发错点，已登记词族候选）；competent vs qualified / capable / proficient（并记「merely competent」的贬义语用）；**faucet（美） vs tap（英）**，拼读 au=/ɔː/、-et=/ɪt/
- **备注（环境限制）**：出网仍被 sinkhole（先 `Resolve-DnsName` 复测确认解析仍指向 198.18.0.0/15，`Invoke-WebRequest` 与 `web_fetch` 均失败），etymonline 不可达——三词的年代/理据细节逐条标「待验证」
- **核对债务**：待回补清单累计 5 词（unto / endometriosis / sew / competent / faucet），已在 hub 显式标记「债务在累积」，待恢复出网后一次性清账
- 更新：[[english-vocabulary]]（进度 12→15、待回补清单列全、新增同音簇词族候选）、`index.md`（Stats：vocab 12→15）
- **更正上一条（第六批）**：占位 wikilink `[[other-word]]` **只存在于 `templates/vocab.md:30`**，hub 页并无该占位（已 grep 全库确认）——上条「模板与 hub 中的该占位」表述有误，修正为仅模板；`other-word.md` 已从磁盘消失（用户清理），无需再处理

## [2026-10-01] schema | v1.5 词汇系统支持多词单位（短语动词 / 习语）

- 触发：本批 inbox 收进 `wore on`、`in sight`——**首次出现多词单位**，而 §3.4 原文只写「每词一页 `wiki/vocab/<word>.md`」，无命名与 lemma 依据；为免 wiki 层自行发明约定而无 schema 支撑，当批一并立规
- 新规：多词单位同样每词条一页——文件名空格换连字符 kebab-case（`wear-on.md`、`in-sight.md`）；frontmatter `word` 保留空格原形（`"wear on"`）；**lemma 取词典 headword，不取遇到形式**（`wore on` → `wear on`，同 `unraveling` → [[unravel]] 之例）；pos 标 `phr. v.` / `idiom`；建页前先查近形页（`in-sight` vs `insight`、`wear-on` vs `wear`）
- 同步：`CLAUDE.md` §3.4 第 2 步 + §7 追加 v1.5；hub「结构约定」加多词条款与「同名陷阱」提示
- 备注：本变更**源自用户收词行为本身，非用户显式请求**——已在 §7 注明「如不认可可回退」，等用户表态

## [2026-10-01] ingest | vocab: 第八批 2 条（wear on / in sight）——首批多词词条

- 来源：`raw/vocab-inbox.md`（《Mattering》）→ src/mattering；去重跳过 15 条
- 新建词条 2 条：[[wear-on]]（遇到形式 `wore on`）、[[in-sight]]
- 词源要点：**wear on**＝wear（古英语 werian「穿、佩戴」← 原始日耳曼语 \*wazjanan ← PIE \*wes-「穿衣」，同族 vest / invest / vestment）＋ on（小品词，表「继续下去」，同 go on / read on / carry on）——「时间继续往前磨」；**in sight**＝in + sight（古英语 sihþ ← 日耳曼语 \*sihtiz ← PIE \*sekʷ-「看」，同族 see / insight / foresight / hindsight）；「临近、在望」义＝目标进入视野的隐喻（故 no end in sight ＝ 尽头不在视野里）
- 易混要点：**wear + 小品词四兄弟** on / off / out / down（含义相去甚远）；**in sight vs insight（只差一个空格！）**、on sight（一见就，shoot on sight）、out of sight、at sight；各登记一条词族候选
- **备注（环境限制）**：出网仍被 sinkhole（复测解析仍为 198.18.0.0/15），两词细节标「待验证」；待回补清单累计 **7** 条
- 更新：[[english-vocabulary]]（进度 15→17、结构约定加多词条款、两条词族候选）、`index.md`（Stats：vocab 15→17）、`CLAUDE.md`（v1.5）
- 另注：根目录出现 `Untitled.canvas`（2 字节，内容 `{}`）——Obsidian 空画布残留；未删除（不静默删用户文件）、未入库，待用户定夺

## [2026-10-01] schema | v1.6 法语词汇系统 + vocab 目录分语言重构（en / fr）

- 触发：用户决定新增**法语**词汇系统（沿用 inbox 收词；条目深度＝阴阳性 + 复数 + 动词变位要点；词源对照 CNRTL），并把词汇目录按语言分轨
- 重构：`git mv` 17 条英语词条 `wiki/vocab/*.md` → `wiki/vocab/en/`（**纯重命名、内容零改动**，独立提交 3ebd3ac，`git show --numstat` 验证 0 插入/0 删除）；`.gitkeep` 迁至 `wiki/vocab/fr/`。wikilink 按 basename 解析（`newLinkFormat: shortest`）——迁移前后 unresolved-link 基线一致（仅 `templates/vocab.md` 的 `[[other-word]]` 一处真断链，本次一并修复为反引号）
- 新增：`templates/vocab-fr.md`（`lang` / `gender` / `plural` 字段 + 「形态要点」章节；动词不列表格）、hub 页 [[french-vocabulary]]（含命名消歧登记表）、收件箱 `raw/vocab-fr-inbox.md`
- schema 同步（CLAUDE.md）：§1 树（vocab/en、vocab/fr）、§2.1（`lang` + `gender` / `plural`）、§2.2（非 ASCII 文件名转写）、§3.4（语言分轨对照表：inbox / 目录 / 模板 / hub / log 标记 `vocab-fr:` / 权威源 CNRTL；法语命名与消歧细则）、§4（双 hub + Stats 格式）、§7（v1.6）
- 词条变更：17 条英语词条补 `lang: en`；闪卡小节标题 `#flashcards` → `#flashcards/en`（语言子牌组，与法语 `#flashcards/fr` 对称；据插件源码子标签自动纳入；排程零风险——迁移前全库无 `SR:` 注释、插件 cardSchedules 为空）
- 幽灵卡修复：模板不再带 `#flashcards` 标签（SRS 插件无模板目录排除，`templates/vocab.md` 的占位卡此前可能被解析为幽灵卡；两个模板均改为注释说明 + 实例页带标签）
- 命名规则要点（法语）：文件名 ASCII 转写（é→e、ç→c、œ→oe、撇号→连字符）；**全库唯一**——跨语言同名加 `-fr`（如 décor → `decor-fr.md`，与 [[decor]] 互链）、同语言近形预置词性后缀（`ou-conj` / `ou-adv`）、避开 Windows 保留名（con / aux / nul）；lemma 取 headword（`suis` → `être`）
- 待办/风险：① 法语词源核对债务随首批词条起累积（出网被 sinkhole 复测确认，一律标「待验证」，登入 [[french-vocabulary]] 待回补清单）；② 幽灵卡修复需在 Obsidian 中核实牌组数（英语应为 17 词条 / 34 卡）；③ `raw/vocab-inbox.md` 内「→ wiki/vocab/」为历史文本，按 §5 规则 1 不改
- 另：根目录 `Untitled.canvas`（空画布残留）经用户确认删除；该文件未入库，删除不影响 git 历史
- 更新：`index.md`（Topics 双 hub、Stats：wiki 页面 16→17、vocab 含 en/fr 分计）、[[english-vocabulary]]（路径、闪卡标签、多词待办句移除、法语互链）、[[personal-knowledge-management]]（页面地图 + 开放问题）

## [2026-10-01] ingest | vocab-fr: 首批 1 词（gouvernement）——法语系统首条词条

- 来源：`raw/vocab-fr-inbox.md`（Duolingo）→ src/duolingo；去重：无既有词条
- 新建词条 1 条：[[gouvernement]]（法语系统首条，`templates/vocab-fr.md` 首次实装）
- 词源要点：gouverner + -ment（拉丁 -mentum）← 拉丁 gubernare「掌舵、治国」← 希腊 kybernan「掌舵」——与 gouvernail（舵）、gouverneur、英语 govern / governor / cybernetics 同源（「治国＝掌舵」隐喻）
- 易混要点：le gouvernement（内阁/行政班子）vs l'État（国家，更广）、la gouvernance（治理）、le régime（政权）；拼读 gou=/ɡu/、-ment=/mɑ̃/
- **备注（环境限制）**：出网仍被 sinkhole，CNRTL 不可达——「12 世纪首见」等年代细节标「待验证」，登入 [[french-vocabulary]] 待回补清单（法语核对债务开账，共 1 条）
- 更新：[[french-vocabulary]]（进度 0→1、待回补开账、新增「掌舵」词族候选）、`index.md`（Stats：fr 0→1）
- 首批观察：v1.6 命名规则（ASCII 转写 / 全库唯一 / Windows 保留名）均未触发消歧——`gouvernement` 无近形与同名冲突

## [2026-10-01] schema | v1.6.1 法语词条新增「英法交叉核对（受影响的英语词）」

- 触发：用户请求——法语词条要找出**受该法语词影响的英语词**做 cross-check
- 新规：法语词条新增「**英法交叉核对（受影响的英语词）**」小节（每词条必做）——分清**借入**（英 ← 法：路径、年代、拼写/读音漂移、词义异同）与**共祖**（同源非借入，勿混）；反向回借（法 ← 英）可留意；英语词库已收录则双向互链；无网络标「待验证」
- 同步：`templates/vocab-fr.md`（新小节 + 闪卡背面「英法交叉」行）、`CLAUDE.md` §3.4 法语要求 + §7（v1.6.1）、hub [[french-vocabulary]]「概述」「结构约定」
- 实装：[[gouvernement]] 新增该小节——英 government / govern / governor / governance ← 古法语本词族（拼写丢 u、词义更宽）；governess 为平行构词；cyber- 共祖非借入；另记「gouvernance 1990 年代从英语回借」待验证
- 备注：英语词库暂未收录 government 等同源词——如后续收词，两页互链；核对债务（CNRTL / etymonline）仍待联网
- 更新：`log.md` 本条；词条 `updated` 保持 2026-10-01（同日多次修订）

## [2026-10-01] ingest | vocab-fr: 第二批 4 词（cathédrale / pâtissier / chapitre / détective）

- 来源：`raw/vocab-fr-inbox.md`（Duolingo）→ src/duolingo；去重跳过 gouvernement
- 新建词条 4 条：[[cathedrale]]、[[patissier]]、[[chapitre]]、[[detective]]——v1.6.1「英法交叉核对」首次批量实装
- 词源要点：**cathédrale**＝拉丁 cathedra「座椅」（← 希腊 kathedra）——主教之座所在之堂；**pâtissier**＝pâte（← 拉丁 pasta ← 希腊 pastē 麦粥/面团）+ -ier；**chapitre**＝拉丁 capitulum「小头」（caput 的指小）——教会「首脑议事会」义由此；**détective**＝**反向回借**（法 ← 英，约 1907）：英语 detective ← detect ← 拉丁 detegere「揭开」= de- + tegere（盖）
- 英法交叉要点：**chair 与 cathedral 同为拉丁 cathedra 的双重借入**；**chief / chef** 同为英语对同一词源的双重借入（caput 家族）；paste / pasta / pâté / pastry 同出拉丁 pasta；detect（揭盖）与 protect（盖住）同根反义
- 异常处理：inbox 首行 `cathedrate`——法语无此词，判定为 **cathédrale** 的拼写变体（**待用户确认**），按 lemma 编译并在词条加「收录说明」；`patissier` / `detective` 为缺重音形式，lemma 按标准拼写（pâtissier / détective）
- 规则细化：跨语言同名消歧改为「**后建页者**加语言后缀」（原规则只写法语 `-fr`；因 [[detective]] 先建、英语 detective 可能后建，补齐对称情形 `-en`）——同步 §3.4 与 hub 结构约定；[[detective]] 预登入 hub 命名消歧登记表
- 更新：[[french-vocabulary]]（进度 1→5、待回补 5 条、词族候选 ×4：caput / cathedra / pasta / 英语回借簇）、`index.md`（Stats：fr 1→5，总 22）
- **备注（环境限制）**：出网仍被 sinkhole（复测 cnrtl.fr 解析仍为 198.18.0.128），年代/路径细节逐条标「待验证」
