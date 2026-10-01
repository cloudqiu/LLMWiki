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
