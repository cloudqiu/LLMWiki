# Index — 知识库目录

> 内容目录（content-oriented）：本库所有页面的清单。每次 ingest 后更新；查询时**先读本文件**找候选页面，再深入具体页面。
> 维护规则见 `AGENTS.md`（Codex）与 `CLAUDE.md`（Claude Code）。最近更新：2026-10-31。

## Sources 来源

- [[llm-wiki-pattern]] — Karpathy《LLM Wiki》gist：模式原始定义，本库创世文档。2026-10-01 摄入，派生 8 个页面。
- [[as-we-may-think]] — Vannevar Bush《As We May Think》(The Atlantic, 1945-07)：memex 与关联索引的一手文献。2026-10-01 摄入，派生/更新 6 个页面。
- [[claude-code-obsidian-tutorial]] — RUNOOB 中文教程：Claude Code + Obsidian 从零搭建 LLM Wiki；含主题/插件清单与目录结构变体。2026-10-01 摄入，新建 3 页、更新 6 页。
- [[windows-terminal-tutorial]] — 光影紐扣科普连载：Windows Terminal 入门——「不是新命令，是新窗口」。**本库首份非 PKM 来源**（OS/开发环境层）。2026-10-06 摄入，新建 8 页、更新 1 页。
- [[dissecting-penpot]] — Penpot 2.18 Docker Compose 安装与镜像检查快照：8 个服务、持久化卷及部署边界。2026-10-21 摄入，派生 2 页。
- [[gophernotes-official-research]] — gophernotes 官方 README 与补全源码的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。
- [[chi-official-research]] — chi v5.5.0 官方文档、仓库与作者项目资料的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。
- [[google-uuid-official-research]] — google/uuid v1.6.0 官方文档、项目沿革与贡献者资料的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。
- [[pgx-official-research]] — pgx v5.12.0 官方文档、变更记录与作者关联项目的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。

## Concepts 概念

- [[llm-wiki]] — 核心模式：LLM 增量维护的持久化 wiki；三层架构 + ingest/query/lint 三操作。
- [[retrieval-augmented-generation]] — RAG：查询时检索切片生成答案，无知识积累。
- [[memex]] — 桌面式私人「文件与图书馆」(1945)：微缩胶片 + 投影屏 + 关联路径。
- [[associative-trails]] — 关联索引/路径：memex 的核心机制；超链接与交叉引用的思想原点。
- [[command-line-interface]] — 命令行界面（CLI）：终端（那扇窗）≠ shell（那个程序）；本地 AI 工具链的执行层。

## Entities 实体

- [[andrej-karpathy]] — AI 研究者；LLM Wiki 模式作者。（stub）
- [[vannevar-bush]] — OSRD 主任（1945）；memex 构想提出者。
- [[obsidian]] — 本地优先的 markdown 知识管理应用；本库的浏览 IDE。
- [[qmd]] — 本地 markdown 搜索引擎（BM25 + 向量 + LLM 重排）。（stub）
- [[claude-code]] — Anthropic 的终端 agent；本库的维护者（「LLM 是程序员」中的程序员）。
- [[runoob]] — 发布本库首份中文教程来源的公众号。（stub）
- [[windows-terminal]] — 微软现代终端模拟器：把 CMD / PowerShell / WSL 装进同一窗口的标签与窗格。
- [[command-prompt]] — Windows 传统命令行 `cmd.exe`：`.bat` 脚本与基础操作。（stub）
- [[powershell]] — 微软现代命令行与脚本环境；AI 工具链在 Windows 上的默认落点。（stub）
- [[wsl]] — Windows Subsystem for Linux：本地 AI 工具（`apt` / `python` / `ollama`）的栖息地。（stub）
- [[winget]] — Windows 命令行包管理器：让「装个新外壳」变成一行可复制的命令。（stub）
- [[guangying-niukou]] — 发布「AI 时代命令行」连载的公众号（署名「凡哥哥」）。（stub）
- [[penpot]] — 可自托管的协作设计平台；本库目前记录其一次 Docker 部署快照。
- [[gophernotes-go]] — Jupyter 的 Go kernel：用途、两个典型代码单元、补全与 Windows 限制。
- [[chi-go]] — Go `net/http` 路由库 chi v5：安装、路径参数、关键限制与作者。
- [[peter-kieltyka]] — chi 作者；索引其在本库已摄入的库及官方资料可核实的其他项目。
- [[google-uuid-go]] — Go UUID 库：生成、解析、格式与随机池的关键限制。
- [[paul-borman]] — google/uuid 贡献者及历史版本发布参与者；索引其账号下的其他 Go 库。
- [[pgx-go]] — PostgreSQL 的 Go 驱动与工具集：基础查询、连接池选用及 v5.12.0 修复。
- [[jack-christensen]] — pgx 原始署名者和近期发布参与者；索引其关联的 PostgreSQL 工具。

## Topics 主题

- [[personal-knowledge-management]] — 个人知识管理：本库正在积累的主题总览（synthesis）。
- [[ai-era-command-line]] — AI 时代的命令行：非技术用户如何搭起本地 AI 工具环境（本轮新开主题 / 连载教程 hub）。
- [[penpot-self-hosting]] — Penpot 2.18 自托管实例的服务拓扑、数据卷与配置注意点。

## Comparisons 对比

- [[llm-wiki-vs-rag]] — 编译式知识 vs. 检索式问答。

## Answers 问答归档

（暂无——有值得留存的查询结果时归档到 `wiki/answers/`）

## Outputs 产物（output/）

（暂无——有产物时登记）

## Library inboxes 第三方库收件箱（raw/）

- [Go 第三方库收件箱](raw/golang-libs-inbox.md) — 每行一个库名；用户要求时再摄入。
- [Rust 第三方库收件箱](raw/rust-libs-inbox.md) — 每行一个库名；用户要求时再摄入。
- [JVM 第三方库收件箱](raw/jvm-libs-inbox.md) — Java / Kotlin 共用；每行一个库名，用户要求时再摄入。

## Backlog 待建页面

- （建议）Engelbart《Augmenting Human Intellect》(1962)：memex → 人机协同的直接后续
- （建议）超文本谱系：Nelson/Xanadu、H.G. Wells《World Brain》(1938)
- （建议）「预测 vs 实现」对照页：memex 的技术预言哪些成真
- （建议）Python / 解释器：「为什么 AI 都爱写 Python」——[[ai-era-command-line]] 系列预告篇（尚未剪藏）
- （建议）Windows Terminal 美化配置：`settings.json`、字体与配色方案（可作 `output/` 产物）
- （待验证）Penpot 实例的登录、文件创建、导出与 MCP 连接；以及其公网暴露、密钥和备份状态
- Obsidian Web Clipper 剪藏流程（方法页）
- Marp 幻灯片 / Dataview 查询用法（工具用法页）
- 搜索方案：qmd 集成评估（wiki 规模增长后再做）
- （评估）raw/ 子目录化（articles / papers）——待来源规模增长后再议（output/ 落盘已于 2026-10-01 采纳，见 schema v1.3）
- （待验证）chi 的当前维护者名单及各自角色；仅凭仓库归属不能推断。
- （待验证）google/uuid 的创始作者与当前维护者名单；Paul Borman 的具体角色已按官方证据限定。
- （待验证）pgx 的完整当前维护者名单，以及用户项目版本与 v5.12.0 安全修复的相关性。

## Stats

- 来源：**9** 份 ｜ wiki 页面：**38** ｜ Outputs：**0** ｜ 最近更新：2026-10-31
