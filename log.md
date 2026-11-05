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

## [2026-10-01] ingest | vocab-fr: 第三批 7 条（il y a / environ / mot / nouveau / auteur / connaître / court）

- 来源：`raw/vocab-fr-inbox.md` → src/duolingo（本批 7 条 inbox **未标注出处**——推断 Duolingo，**待确认**）；去重跳过 5 条（gouvernement / `cathedrate`→cathédrale / patissier / chapitre / detective）
- 新建词条 7 条：[[il-y-a]]、[[environ]]、[[mot]]、[[nouveau]]、[[auteur]]、[[connaitre]]、[[court]]——含法语系统**首条多词单位**（il y a → `il-y-a.md`）
- lemma / 异常处理：`neuveaux` 非法语词 → 判定为 nouveaux（nouveau 阳复）笔误、归并 [[nouveau]]；`connais`（je/tu 现在时）→ 不定式 [[connaitre]]；`court` 有歧义（形容词「短的」/ 网球场 / courir 第三人称）→ 按最可能教学词「短的」编译、另两义在易混中说明——均加「收录说明」并待用户确认
- 词源要点：**il y a**＝il + y（拉丁 ibi「那里」）+ a（avoir ← habere）＝「那里有」——与英 there is 语法化路径同构；**mot**＝拉丁 muttum「嘟囔声」→ 法语把「一声嘀咕」抬成「词」，verbum 分化为 verbe/parole；**nouveau**＝拉丁 novellus（novus「新」指小）；**auteur**＝拉丁 auctor ← augere「增加」——「使作品生长出来的人」；**connaître**＝拉丁 cognoscere ← PIE \*gneh₃-（与英 know 同源）；**court**＝拉丁 curtus「截短」← PIE \*(s)ker-「切」
- 英法交叉要点（本批亮点，借入 vs 共祖样本）：**new（共祖）vs novel（古法语借入）**；**know / can（共祖）vs connoisseur（法语借入，1714）**；**auteur / author 双重借入（doublet）**；**environs / environment ← 法语**；**bon mot / mot juste ← 法语**；**curt 拉丁直借 vs court 经古法语（借的是 cour，另一词源）**
- 更新：[[french-vocabulary]]（进度 5→12、待回补 12 条、词族候选 ×3：connaître/savoir、court·cour·cours、nouveau·neuf·récent+new/novel）、`index.md`（Stats：fr 5→12，总 29）
- **备注（环境限制）**：出网仍被 sinkhole（复测 cnrtl.fr 解析 198.18.0.132），法语词源核对债务累计 **12** 条，待联网一并清账

## [2026-10-01] ingest | vocab-fr: 第四批 14 条 → 12 词条（présentateur / certain / trouver / émission / découvrir / incroyable / déjà / voir / littérature / moderne / prendre / ça）

- 来源：`raw/vocab-fr-inbox.md` → src/duolingo（本批 inbox **未标注出处**——推断 Duolingo，**待确认**）；去重跳过 12 条（前 12 均已编译）
- 新建词条 12 条：[[presentateur]]、[[certain]]、[[trouver]]、[[emission]]、[[decouvrir]]、[[incroyable]]、[[deja]]、[[voir]]、[[litterature]]、[[moderne]]、[[prendre]]、[[ca]]；另补 [[auteur]]（并入 `autrice`）
- **lemma / 归并**：`presentateur` + `presentatrice` 合并为 [[presentateur]]（-teur/-trice 阴性格配，一页承载）；`autrice` 并入 [[auteur]]（阴性形式）；`trouve`→[[trouver]]、`decouvert`→[[decouvrir]]、`vu`→[[voir]]（动词变位形式归不定式）；`deja`/`emission`/`litterature` 补重音、`ca` 补软音符
- 词源要点：**trouver**＝通俗拉丁 *tropare「作诗寻章」← 希腊 tropos——「找到」由「寻得妙句」泛化；**émission**＝拉丁 emittere（ex- 出 + mittere 送）——「节目」义英语没有（**faux ami**）；**déjà**＝des ja（dès + 拉丁 jam「已经」）——与 jamais 同根反义；**voir**＝拉丁 videre ← PIE \*weid-（看/知一体两面）；**prendre**＝拉丁 prehendere「抓」——一「抓」串起拿/吃/乘/花五义；**ça**＝cela 的口语缩合
- 英法交叉亮点：**trove**（= 法语 trouvé）← treasure trove；**discover / cover / covert** ← 古法语 descovrir/covrir；**déjà vu** ← 法语（1903）；**view / voyeur** ← 法语 veoir/voir；**entrepreneur / surprise（-prise = 抓）**；**modern ← 法语 moderne**
- 更新：[[french-vocabulary]]（进度 12→24、待回补 24 条、词族候选 ×3：prehendere「抓」、videre「看/知」、credere「信」）、`index.md`（Stats：fr 12→24，总 41）
- **备注（环境限制）**：出网仍被 sinkhole（复测 cnrtl.fr 198.18.0.132、etymonline 198.18.0.112），法语词源核对债务累计 **24** 条

## [2026-10-01] setup | .gitignore 忽略 Untitled.canvas（Obsidian 空白画布残留）

- 成因：Obsidian 打开空白 canvas 会自动在仓库根目录生成 `Untitled.canvas`（此前数次出现，内容为 `{}` 空画布，非 wiki 内容，已多次手动删除）
- 处理：`.gitignore` 增 `Untitled.canvas`（仅忽略默认空白名）；**不忽略 `*.canvas`**——canvas 是 schema §3.2 认可的合法产出形式，有意创建的画布仍应入库
- 影响：仅版本管理层面，不涉及 wiki 页面与 index/log 计数

## [2026-10-01] ingest | vocab-fr: 第五批 15 条 → 14 词条（mon / frère / chercher / son / déodorant / pouvoir / jamais / rester / longtemps / souffle / bougie / gâteau / sur / inacceptable）

- 来源：`raw/vocab-fr-inbox.md` → src/duolingo（本批 inbox **未标注出处**——推断 Duolingo，**待确认**）；去重跳过 24 条
- 新建词条 14 条：[[mon]]、[[frere]]、[[chercher]]、[[son]]、[[deodorant]]、[[pouvoir]]、[[jamais]]、[[rester]]、[[longtemps]]、[[souffle]]、[[bougie]]、[[gateau]]、[[sur-prep]]、[[inacceptable]]
- **lemma / 归并**：`frere`/`gateau`/`deodorant` 补重音；`cherche`→[[chercher]]、`peut`→[[pouvoir]]（动词形式归不定式）；`son`（主有/声音）与 `souffle`（气息/动词形）为同形双义，各并一页；`sur` 按命名消歧规则记 `sur-prep.md`（与 sûr 近形对，登入命名登记表）
- **句子处理**：inbox 出现整句 `elle ne peut jamais y rester longtemps`——非 headword，不建页，拆解为 pouvoir/jamais/y/rester/longtemps（均已收），并在 [[rester]] / [[longtemps]] 词条中作为例句复用
- 词源亮点：**chercher**＝晚期拉丁 circare「绕行」← circum「环绕」——「找」＝绕圈巡视，英 search 即其借入；**bougie**＝地名 Béjaïa（蜡烛贸易港）→ 通名，英俚语 bougie（← bourgeois）与之**无关**（词源陷阱）；**gâteau**＝古法语 gastel ← 法兰克语（法语里少见的日耳曼词），与英 cake 不同源；**rester**＝re- + stare「站」→ 英 rest/arrest 借入；**pouvoir**＝拉丁 posse（pot- + esse）→ 英 power 借入；**son**（声音）→ 英 sound
- 英法交叉亮点：**sound ← 古法语 son**；**friar ← 古法语 frere**（vs brother 共祖）；**search/research ← 古法语 cerchier**；**déodorant ← 英 deodorant（反向回借）**；**jamais vu ← 法语**（déjà vu 的反面）；**inacceptable（法 in-）vs unacceptable（英 un-）平行构词**；**soufflé / gateau / surface / power 各为其法语源词的英语借入**
- 更新：[[french-vocabulary]]（进度 24→38、待回补 38 条、命名消歧登记表 +sur-prep、词族候选 ×3：capere「拿」、主有词 mon/ton/son、stare「站」）、`index.md`（Stats：fr 24→38，总 55）
- **备注（环境限制）**：出网仍被 sinkhole（复测 cnrtl.fr 198.18.0.132），法语词源核对债务累计 **38** 条

## [2026-10-01] schema | v1.7 词汇系统迁出 → 独立库 LLMLangWiki

- 触发：用户决定把英语 / 法语词汇系统整体迁出为独立语言专库 `C:\Users\zhenz\Documents\LLMLangWiki`（拼写为用户选定）；词汇今后只在新库维护，避免双份分叉
- 迁出方式：整仓复制 + SHA256 全量校验（逐字节一致）后，本库以 `git rm` 移除——55 词条（en 17 / fr 38）、hub `english-vocabulary` / `french-vocabulary`、`templates/vocab.md` / `vocab-fr.md`、`raw/vocab-inbox.md` / `vocab-fr-inbox.md`、产物 `output/2026-10-01-vocab-quiz-01.md`（topic / answer 模板与 `output/README.md` 系复制副本，本库保留原文件）
- inbox 说明：`raw/vocab-*.md` 系按用户决定的整仓迁出，内容逐字未改——硬性规则 1 的对象是内容而非位置；此后收词在新库进行
- schema 同步（本文件，v1.7）：§3.4 整节移除；§1 树、§2.1（vocab frontmatter）、§2.2（法语细则指引）、§4（vocab 例外与 Stats 格式）相应回退；§7 追加本记录
- 页面同步：`index.md`（Topics −2、Outputs → 占位、Stats：3 来源 / 15 页 / 0 产物）；[[personal-knowledge-management]]（页面地图 −2 行；记忆方法开放问题改为「已落地并迁出」）
- 历史保留：本 log 旧条目与 §7 旧记录原文不动——其中词条链接自此悬空（指向已迁出页面），属历史记录不追改；新库 log 已逐字继承 22 条词汇条目（含继承说明）
- 新库侧：git 全新初始化（首次提交见其 log「setup | LLMLangWiki 建库」条目）；SRS `dataStore=NOTES` 无独立排程数据，Obsidian 打开新库即用
- 待办：新库联网后清账两语「待回补」清单（en 7 条 etymonline ｜ fr 38 条 CNRTL）

## [2026-10-06] ingest | Windows Terminal：把黑框变好看（光影紐扣）——本库首份非 PKM 来源

- 来源：`raw/Windows Terminal：把黑框变好看.md`（用户剪藏入库，微信 mp.weixin.qq.com；原文署 Oct 4, 2026）
- 内容：面向非技术读者的终端科普——[[windows-terminal]] 不替代 CMD/PowerShell/WSL，只做「统一外壳」；核心命题「不是新命令，是新窗口」（L162）；附快捷键「命令卡片」（含 🟢/🟡 危险等级）
- 新建页面 8：来源 [[windows-terminal-tutorial]]；实体 [[windows-terminal]]、[[command-prompt]]、[[powershell]]、[[wsl]]、[[winget]]、[[guangying-niukou]]；概念 [[command-line-interface]]（终端 ≠ shell）；主题 [[ai-era-command-line]]（该中文连载的 hub）
- 更新页面 1：[[claude-code]]（补「宿主环境」链接：终端 agent 运行在某个 shell / 外壳里），并把本来源计入其 `sources`
- **联网核对（本机出网对 learn.microsoft.com 与 raw.githubusercontent.com 仍被拦截；经 WebSearch 索引间接核对）**：
  - ✓「Windows 11 自带」与「设置 → 启动 → 默认终端应用程序」路径：与官方一致（Win11 22H2 起 WT 为默认命令行体验，需 WT ≥ 1.15）
  - ⚠️ **矛盾（原文 vs 微软默认键位）**：原文记 `Alt+Shift++` 为「分屏（上下）」；当前默认为 `alt+shift+plus` → **向右**复制窗格、`alt+shift+-` → 向下、`alt+shift+d` → `DuplicatePaneAuto`（方向自动）。已在 [[windows-terminal]] 与来源页双方用 `> [!warning] 矛盾` 标注，不折中
  - ➕ 原文未提但关键：`Ctrl+C` 仅在**有选中内容**时是复制，否则为中断信号（新手最易踩）
  - 待验证项：`winget install Microsoft.WindowsTerminal` 简写 vs 官方 `--id … -e`；`Ctrl+V` 直接粘贴的启用版本；署名「凡哥哥」与公众号「光影紐扣」的对应关系
- schema：**本次未改动**——新页均为既有六类目录内的常规增行，`index` 按类型分区无需新增结构；「主题边界是否扩张」属待用户决议事项，决议前不写入 schema
- 派生：`index.md`（Sources/Concepts/Entities/Topics 各增行，Backlog +3，Stats：4 来源 / 24 页 / 0 产物）
- **待用户决议**：① 本库主题边界是否扩到「OS / 开发环境层」（否则建议按词汇系统先例整体迁出）；② 是否回补该连载前几周文章（预告第三周为 Python 篇）

## [2026-10-06] query | 后续决议：不回补连载前文、不调整本机终端配置

- 触发：ingest 后向用户提出三问，用户答「no need」
- 决议（已回写各页，避免成为 lint 时的「过时开放问题」）：
  - **不回补**该连载前几周文章——[[ai-era-command-line]] 脉络以本篇（「第二周末」）为起点，前史留白；[[windows-terminal-tutorial]] 同类「讨论问题」小节同步标为已决议
  - **不做**本机默认终端 / settings.json 外观调整——[[windows-terminal]] 美化配置仍留在 Backlog，需要时再取
  - 主题边界：用户**未要求迁出** → 本主题维持纳入本库（页面留存）；[[ai-era-command-line]] 的开放问题已注明触发再议的条件
- 更新：`index.md`（Backlog 删「回补前文」一条，其余不变；Stats 不变）；[[windows-terminal-tutorial]]、[[ai-era-command-line]]（当日修订，`updated` 均为 2026-10-06）
## [2026-10-21] schema | 迁移维护规则至 AGENTS.md

- 将 `CLAUDE.md` 改为 `AGENTS.md`，使 Codex 读取本库的 Schema 指令；当前维护者及工作流指称同步更新，历史演进记录保留。
- 更新 `index.md` 的维护规则入口与最近更新日期。
- 修正 7 个 wiki 页面中指向当前 Schema 的链接或维护者描述，并更新其 `updated` 日期；原始资料的引文与历史记录保持原样。

## [2026-10-21] schema | 保留 Claude Code 的维护规则

- 应用户要求，从迁移前的版本恢复 `CLAUDE.md`；该文件与 Codex 使用的 `AGENTS.md` 并存。
- 修正 `AGENTS.md` 的维护者与目录说明、`index.md` 的规则入口，以及 [[claude-code]] 的当前角色描述。前一条 schema 记录中的「改为」不再表示删除原文件。

## [2026-10-21] ingest | Dissecting Penpot：Docker 部署与镜像检查

- 来源：`raw/Dissecting penpot.md`（原文件不改）；2026-10-21 摄入，记录 Penpot 2.18 Compose 配置、启动输出、Valkey Dockerfile 与各镜像检查元数据。
- 新建 3 页：[[dissecting-penpot]]（来源摘要）、[[penpot]]（实体）、[[penpot-self-hosting]]（自托管拓扑与运维边界）。
- 核对官方 Docker 安装与配置文档：确认 2.18 引入 admin-console、默认两份持久化卷需要备份、对外部署建议 HTTPS；页面将官方指南作为辅助核对，而非把个人笔记误称为官方原文。
- 证据边界：原记录仅显示容器 Started / Healthy，应用层功能待验证；示例中关闭安全 Cookie 与邮件验证，使用示例密钥和数据库密码，尚不能据此推断实例已对外暴露。
- 更新 `index.md`：来源 4→5，wiki 页面 24→27；Backlog 增加实例功能与部署状态核实事项。
- 待办：由用户决定下一轮深入服务通信、镜像构成、MCP 集成或可复现的部署与备份流程。

## [2026-10-31] schema | 第三方库收件箱与按需摄入

- 新建 `raw/golang-libs-inbox.md`、`raw/rust-libs-inbox.md`、`raw/jvm-libs-inbox.md`，供用户每行填一个库名；当前均为空，尚未摄入任何库。
- 更新 `AGENTS.md`：约定仅在用户要求时摄入，优先官方来源并存原始资料，库页只保留用途、依赖、1–3 个典型示例和关键限制；收件箱作为用户输入例外。
- 新建 `templates/library.md`；更新 `index.md` 的收件箱导航，来源数与 wiki 页数不变。
- 待办：用户填入库名并提出摄入请求后，按指定范围逐项核查与建页。

## [2026-10-31] ingest | gophernotes（Go）

- 用户说「ingest this」；三个库收件箱均为空。根据连续对话与其此前浏览的 gophernotes 官方仓库，将「this」解释为 gophernotes；未改动收件箱。
- 核对官方 README 与 `complete.go`；本机通过网络代理直接下载 GitHub Raw 失败，因此新建 `raw/gophernotes-official-research-2026-10-31.md` 保存带链接和章节定位的查阅记录，明确它不是官方原文副本。沿用此前的 `raw/gophernotes-usage.md`。
- 新建 [[gophernotes-official-research]]（来源页）与 [[gophernotes-go]]（库页）：记录用途、两个最小示例、补全实现与原生 Windows 导入第三方包的限制；示例和本地补全表现尚未在用户环境验证。
- 更新 `index.md`：来源 5→6，wiki 页面 27→29；待办为用户实际环境的版本、前端与示例验证。

## [2026-10-31] schema | 第三方库摄入增加作者索引

- 更新 `AGENTS.md`：摄入 Go、Rust、JVM 库时核实创建者与当前维护者，建立作者实体页与库页双向链接，并区分本库已摄入的库及有官方依据的其他库。
- 更新 `templates/library.md`，新建 `templates/library-author.md`；身份不明时标待验证并登记 Backlog，其他库的发现不等于摄入。
- 本次未摄入收件箱条目，未改动用户填写的收件箱；`index.md` 的页面清单和计数不变。

## [2026-10-31] ingest | chi v5（Go）与作者 Peter Kieltyka

- 按 §3.4 的默认一次一个规则处理 Go 收件箱首项 `github.com/go-chi/chi/v5`；未改动收件箱，其他条目仍待摄入。
- 查阅 Go Packages v5.5.0、chi 官方 README、Peter Kieltyka 的 GitHub 资料及 webrpc 官方 README。直接下载官方原文受本机网络代理限制，建立 `raw/chi-official-research-2026-10-31.md` 作为带链接的查阅笔记，明确不是原文快照。
- 新建 [[chi-official-research]]、[[chi-go]]、[[peter-kieltyka]]；作者页记录 chi 已摄入，以及尚未摄入的 webrpc、go-llm 线索，区分其可证实的角色。chi 当前维护者身份标为待验证。
- 更新 `index.md`：来源 6→7，wiki 页面 29→32，Backlog 增加维护者核实事项。示例依据官方 API 编写，未实际运行。

## [2026-10-31] ingest | google/uuid（Go）与贡献者 Paul Borman

- 按 §3.4 默认一次一个规则处理 Go 收件箱下一项 `github.com/google/uuid`；收件箱本身未改动。
- 查阅官方 README、Go Packages v1.6.0、CONTRIBUTORS、Releases，以及上游 `pborman/uuid` 和 `pborman/getopt`。直接下载官方原文受本机网络代理限制，建立 `raw/google-uuid-official-research-2026-10-31.md` 作为带链接的查阅笔记，明确不是原文快照。
- 新建 [[google-uuid-official-research]]、[[google-uuid-go]]、[[paul-borman]]；人物页区分已摄入库与未摄入项目，Paul 的身份限定为官方列名贡献者及历史发布参与者，不推断唯一作者或当前维护者。
- 更新 `index.md`：来源 7→8，wiki 页面 32→35；创始作者与当前维护者列入 Backlog。示例依据官方 API 编写，未实际运行。

## [2026-10-31] ingest | pgx v5（Go）与 Jack Christensen

- 按 §3.4 默认一次一个规则处理 Go 收件箱下一项 `github.com/jackc/pgx/v5`；收件箱本身未改动。
- 查阅 pgx 官方 README、Go Packages v5.12.0、v5.12.0 CHANGELOG、LICENSE、发布 tag 和 Jack Christensen 的项目主页；直接下载官方原文受本机网络代理限制，建立 `raw/pgx-official-research-2026-10-31.md` 作为带链接的查阅笔记，明确不是原文快照。
- 新建 [[pgx-official-research]]、[[pgx-go]]、[[jack-christensen]]；库页记录连接、单连接并发边界与 v5.12.0 两项有条件的安全修复。作者页区分 pgx 已摄入与 tern、pglogrepl、pgerrcode 尚未摄入，并限定 Jack 的已证实角色。
- 更新 `index.md`：来源 8→9，wiki 页面 35→38；Backlog 增加完整维护者名单及用户项目版本核实。示例依据官方 API 编写，未实际运行。

## [2026-10-31] ingest | koanf TOML parser v2（Go）与 Kailash Nadh

- 按 §3.4 默认一次一个规则处理 Go 收件箱下一项 `github.com/knadh/koanf/parsers/toml/v2`；未改动收件箱及其中其他条目。
- 查阅 Go Packages v2.2.2、对应 tag 的官方源码、koanf README 与 LICENSE、Kailash Nadh 账号及同账号下其他 Go 项目。直接下载官方原文受本机网络代理限制，建立 `raw/koanf-toml-v2-official-research-2026-10-31.md` 作为带链接的查阅笔记，明确不是原文快照。
- 新建 [[koanf-toml-v2-official-research]]、[[koanf-toml-v2-go]]、[[kailash-nadh]]；区分 parser、koanf 核心和 provider 的模块边界，以及项目原始署名与子模块具体作者的不确定性。作者页列出尚未摄入的 koanf 核心、goyesql 和 stuffbin。
- 更新 `index.md`：来源 9→10，wiki 页面 38→41；Backlog 增加 parser 子模块作者和维护者核实。示例依据官方 API 编写，未实际运行。

## [2026-10-31] ingest | Go 收件箱余下 20 个模块

- 新建 20 份官方资料查阅记录、20 个来源摘要页、20 个库实体页；每页记录用途、依赖、示例、作者归属和限制。
- 将收件箱两处拼写错误映射到官方模块路径，但未修改用户的 raw 收件箱。etcd 模块根路径与 API 子包、do v1/v2 边界均显式注明。
- 相关作者索引与 index.md 同步；示例未在本机执行，版本需按目标 go.mod 核对。
- 新建 5 个可核实个人账号作者页和 6 个组织项目索引页；更新 Jack Christensen、Kailash Nadh 的已摄入库列表。
- 尚不能从官方资料证明的个人创建者及维护者已列入 index Backlog，未把组织仓库归属写成唯一作者。
- 补充 perks 的 Blake Mizerany 原始版权署名与 Björn Rabenstein 当前仓库账号索引，未推断其各自的维护范围。

## [2026-11-01] ingest | koanf file provider（Go）

- 按收件箱默认一次一个规则处理下一项 `github.com/knadh/koanf/providers/file`；未改动用户收件箱或 Obsidian 状态文件。
- 查阅 Go Packages、koanf README、file provider 源码与 go.mod、LICENSE 和 Kailash Nadh 资料；新建 `raw/koanf-file-go-official-research-2026-11-01.md`（查阅笔记，非官方原文副本）、[[koanf-file-go-official-research]]、[[koanf-file-go]]；更新 [[kailash-nadh]]。
- 明确 file provider 只读取原始字节，需配合 parser；README 与当前源码对监听回调事件有差异，目标版本待核。示例未运行；子模块具体作者和完整维护者名单待验证。
- 更新 `index.md`：来源 30→31，wiki 页面 94→96；其余收件箱条目继续待摄入。

## [2026-11-01] ingest | Go 收件箱剩余 18 个模块

- 用户明确要求批量摄入所有 Go 库；此前 25 项已在库中，本次处理收件箱剩余 18 项。收件箱和 Obsidian 状态文件未改动。
- 新建 18 份 `raw/` 官方资料查阅笔记、18 个来源页、18 个库页；核对官方模块路径、典型 API、重要限制，示例均未在目标环境运行。
- 将收件箱 `pelleiter/go-toml/v2` 映射到官方 `pelletier/go-toml/v2`；goautoneg 记录为原项目镜像；Go YAML v2 记录官方停止维护与仓库归档；mitchellh 两个仓库记录归档状态。
- 新建 5 个可核实人物或项目组织索引，更新 [[etcd-io]]、`index.md`；来源 31→49，wiki 页面 96→137。个人作者与完整当前维护者缺乏可靠证据者保留待验证。

## [2026-11-01] ingest | 延迟分位数与单、多实例 P99 示例

- 摄入用户新放入 `raw/为什么只关心p50 p90 p99.md`、`raw/单实例模拟P99.md`、`raw/多实例P99例子.md`；原文未修改，作者和原始发表时间未标注。
- 新建 3 个来源页 [[latency-percentiles-notes]]、[[single-instance-p99-simulation]]、[[multi-instance-p99-examples]]，以及 2 个概念页 [[latency-percentiles]]、[[distributed-quantiles]]；更新 [[perks-go]]、`index.md`。
- 核对官方包文档：perks `Count()` 存在、targeted epsilon 为分位位置绝对误差、`Merge` 明确损坏；caio/go-tdigest 示例所用构造 API 不符；Prometheus Histogram 跨实例查询须聚合桶。原资料“完整可运行”及数值输出均未在本机验证。
- 目录计数：来源 49→52，wiki 页面 137→142。待办：按用户目标环境另行编写和运行修正版示例。

## [2026-11-01] lint | 结构、来源与 P99 交叉引用巡检

- 新建 `output/2026-11-01-lint.md`：检查 142 个 wiki 页面、52 个来源页及 57 个 raw Markdown 文件；未发现缺页 wikilink、孤立页、缺失来源文件或未登记 wiki 页。
- 标出 2 份未摄入的 raw 资料及 43 个未运行的 Go 库示例；近期 P99 的 `perks.Merge` 冲突已在多处显式标注。本轮未重新验证全部外部网页或编译示例。
- 更新 [[prometheus-client-golang-go]] 的 `[[distributed-quantiles]]` 反向链接与来源；`index.md` 登记报告、Backlog 候选，Outputs 0→1；raw 和用户收件箱未改。

## [2026-11-01] ingest | Go 第三方库收件箱新增 17 项

- 按用户明确请求批量摄入 17 项：新增 17 份 `raw/` 官方资料查阅笔记、17 个来源页、17 个库页、4 个作者或组织索引；收件箱与 Obsidian 状态文件未改。
- 将收件箱 `github.com/AlwxSin/nolineerr` 映射至官方 `github.com/AlwxSin/noinlineerr`；记录 garif 文档中的旧 import、go-errorlint GitHub 仓库迁移与 golangci-lint v2 路径。
- 示例未在本机编译或运行；无法可靠确认的个人创建者、现任维护者与部分独立 CLI 用法保留待验证。
- 更新 `index.md`：来源 52→69，wiki 页面 142→180，Outputs 保持 1。

## [2026-11-01] ingest | Go 收件箱新增 22 项

- 按用户请求批量摄入收件箱新增 22 项：新建 22 份原始资料查阅记录、22 个来源页、22 个库页、5 个身份索引；原收件箱未修改。
- 将 `github.com/alignse/ninnesser` 映射到官方 `github.com/alingse/nilnesserr`；对 /v2、CLI 安装路径和外部 Sass 运行时的边界做显式标注。
- 用法示例均未在本机运行；不确定的个人作者或当前维护者保留待验证。
- `index.md` 统计：来源 69→91；wiki 页面 180→229；Outputs 保持 1。

## [2026-11-01] ingest | raw 中剩余 3 份正文资料

- 摄入 `raw/为什么外企Leadership越来越看重员工的Emotional Control？.md`、`raw/告别混淆！Rust Cell 家族：从 UnsafeCell 到 Cell、RefCell、OnceCell、LazyCell.md` 和 `raw/微信为什么使用 SQLite 保存聊天记录？.md`；原件未修改。Rust/JVM 库收件箱暂无条目，Go 收件箱已在前两批处理。
- 新建 3 个来源页和 3 个概念页；更新 `index.md`。来源 91→94、wiki 页面 229→235、Outputs 保持 1。
- 关键决定：微信标题文章正文实际为 Markus Winand 的 SQLite 2018 SQL 功能转载，不把它当作微信存储实现证据；其普通聚合 FILTER 限制已被 SQLite 3.30.0 推翻，来源页与概念页双向标注。Rust Cell 家族以官方文档核对运行时借用和版本边界；Emotional Control 的因果推断保留为作者观点。
- 待办：寻找微信存储的一手资料；补职场沟通的实证研究。剪藏文章的原始发表时间与部分作者身份待验证。

## [2026-11-01] ingest | Go 收件箱新增 18 项

- 用户明确要求批量摄入新增 18 项；新建 18 份官方资料查阅笔记、18 个来源页、18 个库页和 9 个经官方账号核实的身份索引；更新 [[charmbracelet]]、`index.md` 与本日志。
- Charm 的 5 个 x 子模块按独立 Go module 路径记录，并注明实验性与平台边界；zxcvbn-go 记录活跃 fork 与原仓库归档关系。
- 所有示例未在目标环境编译或运行；作者/现任维护者无法由仓库归属单独推断，故保留待验证。收件箱与 Obsidian 状态文件未改。
- 来源 94→112，wiki 页面 235→280，Outputs 保持 1。

## [2026-11-01] ingest | Go 收件箱后续 45 个新库

- 收件箱新增 46 行中，`github.com/go-viper/mapstructure/v2` 已摄入；本次为其余 45 项新增 45 份官方仓库查阅笔记、45 个来源页、45 个库页及 7 个官方仓库账号索引。更新 `index.md` 与本日志；收件箱原文未改。
- 明确记录 `golang/protobuf` 被新模块取代、`golangci/golines` 的 fork 状态、`gohugoio/hashstructure` 的 fork 状态、HCL v2 不兼容 v1，以及若干 golangci 集成仓库的边界。
- 将收件箱的 `go-toolsmith/astformat` 对应到官方 `go-toolsmith/astfmt`，并将 `hashicorp/hcl` 的依赖路径核对为 `/v2`；收件箱原文不变。
- 示例未在本机编译或运行；缺少可确认独立 API 示例的页面标为 stub，个人作者及现任维护者待验证。用户已有 wiki 页面和 Obsidian 状态修改未纳入本批。
- 来源 112→157，wiki 页面 280→377，Outputs 保持 1。

## [2026-11-01] ingest | Go 收件箱后续 42 个可核实库

- 本轮收件箱在上一批后新增 43 行；42 项找到可靠官方仓库或包文档，新增 42 份 raw 查阅笔记、42 个来源页、42 个库页及 5 个账号索引，并更新 [[mitchell-hashimoto]]、`index.md` 与本日志。原收件箱未修改。
- 将 `copyloader`→`copyloopvar`、`testableexemples`→`testableexamples`、`predecalred`→`predeclared`、`rogpeople`→`rogpeppe` 显式映射；两个 quasilyte 子包按所属模块记录。
- `github.com/ldez/girgnotin` 无法可靠辨认，保留在 Backlog，不作为已摄入库。部分库缺少可确认最小 API 示例而标 stub；其余示例未在本机运行。个人创建者及现任维护者待核实。
- 来源 157→199，wiki 页面 377→466，Outputs 保持 1。

## [2026-11-01] ingest | Grignotin 路径消歧与补摄入

- 用户补充 `github.com/ldex/grignotin` 后核对官方仓库，确认实际路径为 `github.com/ldez/grignotin`；收件箱原条目 `github.com/ldez/girgnotin` 未修改。
- 新增 `raw/ldez-grignotin-go-official-research-2026-11-01.md`、[[ldez-grignotin-go-official-research]]、[[ldez-grignotin-go]]；更新 [[ldez-account]]、`index.md` 和本日志。示例对照官方 README，未在本机运行；具体个人作者及维护角色待验证。
- 来源 199→200，wiki 页面 466→468，Outputs 保持 1；本批 43 个新增收件箱条目均已归档或明确消歧。

## [2026-11-01] ingest | Go 收件箱后续 36 项

- 用户要求批量摄入；收件箱在上一批后新增 36 项。本次新建 36 份 raw 官方资料查阅笔记、36 个来源页、36 个库页及 4 个账号/作者索引，更新 `index.md` 与本日志；收件箱未修改。
- 将 `ssgrep/nlreturn/v2` 对应到官方 `ssgreg/nlreturn/v2`，`ultraware/wihtespace` 对应到 `ultraware/whitespace`；`ryancurrah/gomodguard/v2` 按官方 v2 CLI 子模块 `ryancurrah/gomodguard/cmd/gomodguard/v2` 记录。
- 版本边界：`jsonschema/v6` 使用 v6 包文档；Logrus 维护模式、Testify v1 维护策略按项目 README 记录。所有示例未在本机运行；个人创建及现任维护者未由仓库归属推断。
- 来源 200→236，wiki 页面 468→544，Outputs 保持 1。

## [2026-11-01] ingest | Rust 收件箱 49 项

- 用户要求批量摄入 Rust 收件箱全部 49 项；按 docs.rs 发布文档核对 crate 名称、用途与显示版本，新建 49 份 `raw/*-rust-official-research-2026-11-01.md` 查阅笔记、49 个来源页、49 个库页，并更新 `index.md` 与本日志。收件箱原文未改，也未纳入提交。
- `bracktrace` 没有可访问的正式文档，暂映射为有文档的 `backtrace`，在页面与 Backlog 保留待确认事项；`anyhow_ext`、`error-code` 等确有独立 crate，名称中的连字符与 import 下划线已区分。
- 研究笔记是对官方发布文档的整理，不是官方原文副本。示例未在本机编译运行；个人创建者和现任维护者没有足够官方证据时一律标待验证，未凭包 owner 建作者页。低层实现组件缺少可靠独立示例的页面标 stub。
- 来源 236→285，wiki 页面 544→642，Outputs 保持 1。

## [2026-11-01] ingest | Rust 收件箱新增 46 项

- 当前收件箱共 95 行；前次 49 项已摄入，本次新增 46 项。按 docs.rs 发布文档核对名称、用途与显示版本，新建 46 份 raw 查阅笔记、46 个来源页、46 个库页；更新 `index.md` 和本日志。收件箱原文未改，也未纳入提交。
- 用户已把先前的 `bracktrace` 改为 `backtrace`，因此更新 [[backtrace-rust]] 与其来源页，保留旧 raw 查阅记录作为历史。新条目 `jpeg-decorder` 暂按有正式文档的 `jpeg-decoder` 归档，在页面和 Backlog 标记待核对。
- 研究笔记不是官方原文副本；示例未在本机编译运行。没有可靠身份依据的个人创建者和现任维护者标待验证；部分底层组件未找到可核实的独立最小示例，页面标 stub。
- 来源 285→331，wiki 页面 642→734，Outputs 保持 1。

## [2026-11-01] ingest | Rust 收件箱后续 110 项

- 当前收件箱共 205 行；前两批 95 项已摄入，本次新增 110 项。按 docs.rs 发布文档核对名称、用途与显示版本，新建 110 份 raw 查阅笔记、110 个来源页、110 个库页，补同生态交叉链接，并更新 `index.md` 与本日志。收件箱原文未改，也未纳入提交。
- `poetential_utf` 暂对应 `potential_utf`，`singal-hook-registry` 暂对应 `signal-hook-registry`，`sha1-1` 暂对应 `sha1`；上述映射待原始依赖清单确认。`rustls-webpki` 的包名与 Rust 模块名 `webpki` 已区分。`redox_syscall` 主要供 Redox 内核和 relibc 使用；SHA-1 仅宜作旧协议兼容。
- 研究笔记不是官方原文副本；片段未在本机编译运行。个人创建者与现任维护者无可靠官方证据处标待验证；缺少可核实独立示例的底层组件标 stub。
- 来源 331→441，wiki 页面 734→954，Outputs 保持 1。

## [2026-11-01] ingest | Rust 收件箱后续 38 项

- 当前收件箱共 243 行；前几批 205 项已摄入，本次新增 38 项。按 docs.rs 发布文档核对名称、用途与显示版本，新建 38 份 raw 查阅笔记、38 个来源页、38 个库页，补同生态交叉链接，并更新 `index.md` 与本日志。收件箱原文未改，也未纳入提交。
- `utf-8` 的 Rust 模块名为 `utf8`；`webpki` 与 `rustls-webpki` 是不同发布包；`wasm-bindgen-shared` 由 crate 发布页核对。用户已把收件箱中的 `utf9_iter`、`utf9parse` 更正为 `utf8_iter`、`utf8parse`，故无需建立旧拼写页。
- 研究笔记不是官方原文副本；片段未在本机编译运行。个人创建者与现任维护者无可靠官方证据处标待验证；缺少可核实独立示例的底层组件标 stub。
- 来源 441→479，wiki 页面 954→1030，Outputs 保持 1。

## [2026-11-01] schema | 新增 Python 与 npm 第三方包收件箱

- 新建 `raw/python-libs-inbox.md`、`raw/npm-libs-inbox.md` 两个空白用户输入页；更新 `AGENTS.md` §1、§3.4 与 Schema 演进记录，以及 `index.md` 的 Library inboxes 区。`CLAUDE.md` 作为保留的原有 Claude 入口未改。
- Python 收件箱以 PyPI 发布名记录；npm 收件箱保留 scope 原写法。只有明确要求摄入时才研究与建页。来源、wiki 页面与 Outputs 数量未变。

## [2026-11-01] ingest | Python 收件箱 30 项

- 用户要求批量摄入 Python 收件箱全部 30 项；按 PyPI 项目发布页核对名称、用途与可取得的版本，新建 30 份 raw 查阅笔记、30 个来源页、30 个库页，补关联库交叉链接，并更新 `index.md` 与本日志。收件箱原文未改，也未纳入提交。
- 用户已将 `colorma` 更正为 `colorama`，按正式发布名归档。记录了 PyPI 发布页版本，但实际项目版本仍待按依赖锁定文件核对；未从包 owner 或发布者推断创建者和现任维护团队。
- 研究笔记不是官方原文副本，示例未在本机运行；缺少可核实独立最小示例的页面标 stub。另查 PyPI Credits 与作者个人主页，新增 1 份 raw 身份查阅笔记、1 个来源页及 [[alex-gronholm]]、[[sebastian-ramirez]] 两个作者页，并与对应库页双向链接。来源 479→510，wiki 页面 1030→1093，Outputs 保持 1。
## [2026-11-02] ingest | Rust 收件箱新批次 10 项（进行中）

- 按 docs.rs 发布文档核对 aead、aes、aes-gcm、ahash、aho-corasick、allocator-api2、arrayref、arrayvec、async-channel、async-executor 的用途与显示版本；新增各 10 份 raw 研究笔记、来源页、库实体页，并更新 `index.md`。
- 这些页面是 stub：尚需逐项核实独立最小示例、创建者及当前维护者；示例未在本机运行。后续仍需处理 Rust 收件箱其余新增条目与 Go 收件箱末尾新增条目。收件箱条目未因摄入而删除。
- 来源 510→520，wiki 页面 1093→1113，Outputs 保持 1。

## [2026-11-02] ingest | Go 收件箱末尾 11 项

- 按 Go Packages 发布页核对 Go 收件箱末尾 11 个模块的名称、用途和显示版本；各新增一份 raw 查阅笔记、来源页和库实体页，并更新 `index.md`。收件箱条目保留。
- 可从包文档核对的调用入口已记录；其余页面标 stub，等待按具体子包补独立示例。示例未在本机运行；创建者和现任维护者待官方证据核实。
- 来源 520→531，wiki 页面 1113→1135，Outputs 保持 1。Rust 收件箱新增条目仍待继续摄入。

## [2026-11-02] ingest | Rust 收件箱新增段 crates.io 元数据初编

- 对 Rust 收件箱剩余名称逐一查询 crates.io 官方 API；180 个新 crate 建立 raw 研究笔记、来源页与库实体页，更新 `index.md`；原收件箱不删改。
- `unicode-normalilzation` 暂映射为正式发布名 `unicode-normalization`，待按原始依赖清单复核；`tinyvec-macros` 与已有 `tinyvec_macros` 注册表指向同一 crate，沿用原页；`atomic-walker`、`stringgrep` 查询返回 404，留在 Backlog。
- 本批页面均为 stub：已核实发布名称、显示稳定版本和官方摘要，独立 API 示例、创建者、当前维护者仍待补；代码未编译运行。来源 531→711，wiki 页面 1135→1495，Outputs 保持 1。

## [2026-11-02] query | Rust crate 的 -core 拆分与 time/time-core

- 核对 Rust Reference、Cargo Book、time 仓库 Cargo.toml 与 time-core 文档，新增 `raw/rust-core-crate-split-official-research-2026-11-02.md` 研究笔记和 [[rust-crate-core-split]] 答案页；更新 [[time-rust]]、[[time-core-rust]] 的交叉链接以及 `index.md`。
- 区分一般命名惯例与 time 项目的实际依赖关系；time-core 官方明确标为内部实现细节，不把 `-core` 后缀解释成标准库 `core` 或 `no_std` 保证。来源保持 711，wiki 页面 1495→1496，Outputs 保持 1。

## [2026-11-02] query | time 与 time-core 的具体内容和应用依赖

- 核对 docs.rs 的公开类型、模块与 feature，以及 time 的 Cargo.toml；新增 `raw/time-vs-time-core-official-research-2026-11-02.md` 和 [[rust-time-vs-time-core]]，更新 [[time-rust]]、[[time-core-rust]]、`index.md`。
- 明确应用直接使用 `time::...` 时只需声明 `time`；`time-core` 是其内部依赖，官方不建议直接使用。来源保持 711，wiki 页面 1496→1497，Outputs 保持 1。

## [2026-11-03] ingest | 《Rust 编程实战》九篇入门剪藏

- 用户明确要求批量摄入九篇；将九份原始剪藏保留于 `raw/`，新建九个 `wiki/sources/` 摘要页与 [[rust-programming-basics]] 主题页，同步更新 `index.md`。未触碰工作区原有的 Obsidian 配置与其他未跟踪文件。
- 剪藏覆盖系列第 1–7、9–10 篇；第 8 篇缺失，列入 Backlog。正文署名与发布日期取自剪藏内容，原 frontmatter 相应字段为空；网页未在线核对。
- 各页保留了安装、Cargo 锁文件、线程安全、类型转换和代码示例的验证边界；教程里的命令与例子未在本次摄入时执行。来源 711→720，wiki 页面 1497→1507，Outputs 保持 1。

## [2026-11-03] ingest | 《Rust 编程实战》控制流四篇

- 用户明确要求批量摄入系列第 11–14 篇；四份原始剪藏存于 `raw/`，新建四个来源摘要页，扩展 [[rust-programming-basics]] 主题页，并同步更新 `index.md`。未改动原始剪藏内容。
- 第 11 篇订单示例先写实付 96.00，随后自行更正为 106.00；第 12 篇预计算循环条件需要在循环中重新求值；第 14 篇 let chain 语法需按目标 Rust 工具链核对。教程代码未在本次摄入时编译运行。
- 第 8 篇仍缺原文。来源 720→724，wiki 页面 1507→1511，Outputs 保持 1。

## [2026-11-04] ingest | 《Rust 编程实战》数组、元组与切片三篇

- 用户确认批量摄入系列第 15–17 篇；保留三份原始剪藏于 `raw/`，新建 [[rust-array-clipping]]、[[rust-tuple-clipping]]、[[rust-slice-clipping]] 来源页，扩展 [[rust-programming-basics]]，并更新 `index.md`。
- 区分数组 `[T; N]`、元组与借用切片 `&[T]` / `&str`；记录直接索引与范围访问的 panic 边界、`get()` 的可选返回，以及 UTF-8 字节边界。教程代码未在本次摄入时编译运行，正文署名与日期未在线核对。
- 第 8 篇仍缺原文。来源 724→727，wiki 页面 1511→1514，Outputs 保持 1。

## [2026-11-04] ingest | 《Rust 编程实战》String 与 Vec 两篇

- 摄入系列第 18–19 篇两份新剪藏；保留 `raw/` 原文，新建 [[rust-string-str-clipping]]、[[rust-vec-clipping]] 来源页，扩展 [[rust-programming-basics]]，补充数组、切片来源页的交叉链接，并同步更新 `index.md`。文末剪藏广告不作为教程证据。
- 记录 `String` / `&str` 的所有权与借用、UTF-8 字节边界、`Vec` 长度与容量、排序去重和队列删除代价。代码未在本次摄入时编译运行；正文署名与日期未在线核对。其他已修改的 raw 文件保持原样。
- 第 8 篇仍缺原文。来源 727→729，wiki 页面 1514→1516，Outputs 保持 1。

## [2026-11-04] ingest | 三份 Rust crate 发现与推荐剪藏

- 将 Rustify 十库文章、blessed.rs 的 Crate List 和 crates.dev 首页剪藏保留于 `raw/`，各建来源页，并新建 [[rust-crate-selection]] 主题页；同步更新 `index.md`。没有将推荐列表误作逐个库的官方摄入。
- 将十个主推荐与本库已有实体页互链；量化普及率、维护状态、站点自称审查及部分术语定义仅作为待核查说法。未在线核对网页现状，也未运行文章示例。
- 来源 729→732，wiki 页面 1516→1520，Outputs 保持 1。已有工作区中的其他 raw 与 Obsidian 修改不纳入本次提交。

## [2026-11-04] query | crates.dev 站点内容摘要

- 查询 [[crates-dev-discovery-clipping]] 与原始首页剪藏，并浏览 crates.dev 首页及其导航直接链接的 23 个不同站内页面；新增 `raw/crates-dev-site-survey-2026-11-04.md` 查阅记录及 [[crates-dev-site-summary]] 答案页，更新 `index.md`。
- 归纳单库评论、主题清单、管理/选型/贡献指南与运行时比较；以 Rust、Rocket、rustls、Hyper 官方资料核对部分旧术语和代码示例。未取得 sitemap，不能证明覆盖未链接页面。
- 未摄入站内所列的各个 crate，未运行示例；来源页 732 不变，wiki 页面 1520→1521，Outputs 保持 1。

## [2026-11-04] ingest | Rust 异步生态对话摘录

- 保留 `raw/Rust 异步生态futures，async_std, tokio.md` 原文；新增 [[rust-async-ecosystem-conversation]] 来源页与 [[rust-async-runtime-boundaries]] 概念页，更新 `index.md`。
- 核对 futures、Tokio、async-std、标准库 Future 的发布文档；在新来源页及已有 futures/async-std 实体和官方来源页双向标注冲突：futures 执行器并非只有单线程，async-std 项目已停止并建议转向 smol。
- 原文的示意代码未在本次摄入时编译运行；绝对化的生产环境与运行时兼容性判断继续标待验证。来源 732→733，wiki 页面 1521→1523，Outputs 保持 1。

## [2026-11-04] ingest | Rust crate smol

- 根据 `raw/rust-libs-inbox.md` 新增的 `smol` 条目，查阅 smol 2.0.2 官方文档、仓库和 manifest；新增 `raw/smol-rust-official-research-2026-11-04.md`、[[smol-rust-official-research]]、[[smol-rust]]、[[stjepan-glavina]]，更新 [[async-executor-rust]]、[[async-std-rust]]、[[rust-async-runtime-boundaries]] 与 `index.md`。收件箱原文未改动。
- 官方 manifest 明确列 Stjepan Glavina 为 smol 与 async-executor 作者；创建者具体角色和当前维护者待验证。记录 `block_on`、`spawn` 两个最小示例及 Tokio 适配边界，示例未在本机编译运行。
- 来源 733→734，wiki 页面 1523→1526，Outputs 保持 1。

## [2026-11-04] query | 系统性学习 Rust Tokio 的指南

- 查阅 Rust Book 与 Tokio 官方教程、API 和专题资料，写入 `raw/tokio-learning-guide-official-research-2026-11-04.md`，归档 [[rust-tokio-systematic-learning-guide]]；更新 [[tokio-rust]] 与 `index.md`。
- 指南按 Rust 基础、运行时与任务、共享状态与通道、网络 I/O、取消关闭及测试观测安排练习，以 Mini-Redis 为贯穿项目；示例未在本机编译运行，API 需按目标 Cargo.lock 核对。
- 来源 734 不变，wiki 页面 1526→1527，Outputs 保持 1；保留 `raw/rust-libs-inbox.md` 的用户编辑。

## [2026-11-04] query | Rust Send + 'static 与 Tokio 任务

- 查阅 Rust 标准库、Rust By Example 和 Tokio `spawn` / `spawn_local` 官方文档，新增 `raw/rust-send-static-tokio-official-research-2026-11-04.md` 与 [[rust-send-static-in-tokio]]，并从 [[rust-tokio-systematic-learning-guide]] 互链；更新 `index.md`。
- 区分 `T: 'static` 与 `&'static T`，用 `async move`、`Arc` 及非 `Send` 值跨 `.await` 的示例说明编译错误；示例未在本机编译。来源 734 不变，wiki 页面 1527→1528，Outputs 保持 1。

## [2026-11-04] query | Send trait 的其他用法

- 查阅 Rust 标准库与 Rustonomicon，新增 `raw/rust-send-other-uses-official-research-2026-11-04.md`；扩展 [[rust-send-static-in-tokio]]，补 `std::thread::spawn`、跨线程 channel、泛型 API、trait object、`Send`/`Sync` 区别及手动 `unsafe impl` 的边界；同步更新 `index.md`。
- `channel<T>()` 本身没有 `T: Send` 约束，跨线程移动通道端点才体现消息的线程安全要求。同步线程/channel 示例已用本机 Rust 1.99.1 编译运行并输出“完成”；来源和 wiki 页面计数不变，Outputs 保持 1；`raw/rust-libs-inbox.md` 用户编辑仍不纳入提交。

## [2026-11-04] query | Rust Sync、trait object 与跨线程智能指针

- 查阅 Rust 标准库、Reference 和 Rust Book，新增 `raw/rust-sync-trait-objects-smart-pointers-official-research-2026-11-04.md` 与 [[rust-sync-trait-objects-thread-safe-pointers]]；从 [[rust-send-static-in-tokio]] 互链并更新 `index.md`。
- 区分 `Send` 的转移与 `Sync` 的共享引用，核对 Box、Arc、Mutex、RwLock、Rc 的泛型条件及 `dyn Trait + Send + Sync`；示例已用 Rust 1.99.1 编译运行并通过断言。来源 734 不变，wiki 页面 1528→1529，Outputs 保持 1。保留 `raw/rust-libs-inbox.md` 用户编辑。

## [2026-11-05] ingest | 《Rust 编程实战》HashMap、Option、Result、错误处理与 Module 五篇

- 用户确认批量摄入系列第 20–22、24–25 篇；保留五份 `raw/` 剪藏原样，新建 [[rust-hashmap-clipping]]、[[rust-option-clipping]]、[[rust-result-clipping]]、[[rust-error-handling-best-practices-clipping]]、[[rust-module-clipping]]，扩展 [[rust-programming-basics]] 并更新 `index.md`。
- 记录 `HashMap` 的 `entry`、所有权与无序遍历，`Option` / `Result` 的缺失值和错误传播，以及模块的路径与可见性。第 24 篇将除数为零设为 panic，与同篇可预期输入错误返回 `Result` 的建议冲突，已在来源页和主题页双向标注。
- 第 8、23 篇尚缺原文；本批示例未编译运行，网页署名与发布日期未在线核对，`thiserror` / `anyhow` 依赖版本待按目标项目核实。来源 734→739，wiki 页面 1529→1534，Outputs 保持 1；其他用户编辑和未跟踪资料保留原状。

## [2026-11-05] ingest | 《Rust 编程实战》Package 与 Crate、use 与 pub 两篇

- 用户确认批量摄入系列第 26–27 篇；保留两份 `raw/` 剪藏原样，新建 [[rust-package-crate-clipping]]、[[rust-use-pub-clipping]]，扩展 [[rust-programming-basics]] 并更新 `index.md`。
- 整理 package、crate、module、workspace、`use`、`pub` 与重新导出之间的关系；记录原文中 workspace member 与 crate 混称、额外 `lib2.rs` target 说明不准确，以及公开 API 示例的路径与模块声明需复核。
- 第 8、23 篇仍缺；本批代码未编译运行，网页署名与发布日期未在线核对。来源 739→741，wiki 页面 1534→1536，Outputs 保持 1；此前已有的收件箱、Obsidian 与 Module 原文工作区变更不纳入本次提交。

## [2026-11-05] query | Rust crate 为什么 re-export 第三方依赖

- 查询 [[rust-use-pub-clipping]]、[[rust-package-crate-clipping]]、[[smol-rust]] 及其 raw 依据；查阅 Rust Book、Reference、Cargo Book、API Guidelines 与 smol 官方文档，记录于 `raw/rust-crate-dependency-reexports-official-research-2026-11-05.md`。归档 [[why-rust-crates-reexport-dependencies]] 并更新 `index.md`。
- 区分统一入口、公开类型的导入路径、兼容路径与 Cargo feature 转发；指出 re-export 不会自动合并不兼容依赖版本，公开依赖会成为 SemVer 责任。未针对用户的具体项目运行 `cargo tree -d`；来源页仍 741，wiki 页面 1536→1537，Outputs 保持 1。

## [2026-11-05] ingest | 《Rust 编程实战》文档、单元测试、集成测试与所有权四篇

- 用户确认批量摄入系列第 28–31 篇；保留四份 `raw/` 剪藏原样，新建 [[rust-rustdoc-cargo-doc-clipping]]、[[rust-unit-testing-clipping]]、[[rust-integration-testing-clipping]]、[[rust-ownership-clipping]]，扩展 [[rust-programming-basics]]、更新 [[rust-error-handling-best-practices-clipping]] 的矛盾提示，并同步 `index.md`。
- 文档与测试两篇把除零设计为 `Result::Err`，与第 24 篇的直接 `panic!` 示例冲突，已在相关来源页和主题页标注；doctest 缺导入、固定临时文件名和 Copy/Move 的栈堆简化表述记录为核对事项。
- 本批示例未编译运行，网页署名和日期未在线核对。第 8、23 篇仍缺；来源 741→745，wiki 页面 1537→1541，Outputs 保持 1。其他工作区修改不纳入本次提交。

## [2026-11-05] query | Rust 函数返回 String 还是 &str

- 查询 [[rust-string-str-clipping]]、[[rust-ownership-clipping]]、[[rust-functions-return-values-clipping]] 及原文；查阅 Rust Book、Reference、标准库和错误解释 E0515，记录于 `raw/rust-string-return-ownership-official-research-2026-11-05.md`。归档 [[rust-function-return-string-or-str]]，更新 `index.md`。
- 按结果是否借自输入、是否需独立拥有区分 `&str` 和 `String`；补充字面量 `&'static str` 与混合返回的 `Cow<'a, str>`，说明不能返回局部 `String` 的借用。示例未在本次编译；来源页仍 745，wiki 页面 1541→1542，Outputs 保持 1。
