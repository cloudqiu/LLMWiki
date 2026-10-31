# gophernotes 官方资料查阅记录（2026-10-31）

本文件是查阅记录，**不是官方 README 原文副本**。本机直接下载 GitHub Raw 失败（网络代理 socket 被权限阻止）；以下仅记录本次实际核对的资料位置与事实，供 wiki 回溯。官方页面仍是最终依据。

## 官方项目 README

- 页面：https://github.com/gopherdata/gophernotes/blob/master/README.md
- 查阅日期：2026-10-31；分支：`master`。README 的安装示例使用 `v0.7.5`；用户本机实际版本未核实。
- `gophernotes` 是供 Jupyter Notebook / nteract 交互执行 Go 的 kernel，底层使用 `gomacro` 解释器。（README 开头）
- 用户在 Jupyter 中选择 Go kernel 后，可逐个代码单元执行 Go 语句。（Getting Started）
- README 的特殊命令列有 `%cd [path]`、`%go111module {on|off}`、`%help` 与 `$ shell_command [args...]`，命令须单独占一行。（Special commands）
- README 指出：原生 Windows 环境下，因 Go `plugin` 限制，不能导入第三方包；需要这类包时建议在 Docker 中运行 gophernotes/Jupyter。（Windows；Limitations）
- 其他解释执行限制见 README 的 Limitations，不能把它视为对所有 Go 代码完全兼容的编译器。

## 官方补全实现

- 页面：https://github.com/gopherdata/gophernotes/blob/master/complete.go
- 查阅日期：2026-10-31；分支：`master`。
- `handleCompleteRequest` 从 Jupyter 请求中读取代码和光标位置，调用 `gomacro` 的 `CompleteWords` 返回候选；无候选时回错误。由此可确认 kernel 提供补全协议，但不能据此保证特定前端会在键入时自动弹出建议。（约第 358–398 行）

## 本次未验证

- 用户机器上的 gophernotes 版本、安装方式、Jupyter 前端及具体补全表现。
- wiki 中的示例是否已在用户的 notebook 中实际运行。
