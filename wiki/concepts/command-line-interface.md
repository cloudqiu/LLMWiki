---
title: 命令行界面（CLI）
type: concept
created: 2026-10-06
updated: 2026-10-06
tags: [command-line, interface, terminal]
status: growing
sources: [raw/Windows Terminal：把黑框变好看.md]
---

# 命令行界面（CLI）

## 定义

> 用文本命令而非图形控件与计算机交互的界面；在 Windows 语境下，它由两层组成：**终端（terminal，那扇窗）** 与 **shell（解释并执行命令的那个程序）**。

## 为什么重要 / 解决什么问题

- [[llm-wiki]] 模式与一切本地 AI 工具链的**执行层**：agent 给的命令最终都要落到某个 shell 里跑，人必须先能分清「我现在在哪个 shell 里」。
- 命令行的心理门槛常被误判为技术门槛。[[windows-terminal-tutorial]] 的主张是：门槛有相当一部分来自**观感与操作别扭**（白字黑底、字体模糊、不能分屏、复制粘贴反直觉），因此改善外壳就能实质降低门槛（原文 L26-28、L142-146）。

## 机制 / 要点

**终端 ≠ shell**——这是 [[windows-terminal-tutorial]] 的核心洞见，也是理解 Windows 命令行生态的钥匙：

| 层 | 是什么 | 例子 |
| --- | --- | --- |
| 终端 / 终端模拟器 | 负责显示与输入的那扇窗 | [[windows-terminal]]、老的 Windows 控制台宿主（conhost） |
| shell | 真正解释并执行命令的程序 | [[command-prompt\|CMD]]、[[powershell]]、[[wsl]] 里的 bash |

由此推出三条推论（原文 L38、L164-172）：

- **换壳不换语义**：装进新终端后，CMD 命令还是 CMD 命令，Linux 命令还是 Linux 命令（原文 L168）。
- **shell 决定命令有效域**：在 PowerShell 标签里粘贴 Linux 命令，照样报错——「先看标签页名字，再粘贴」（原文 L170-172）。
- **多 shell 并存是常态**：AI 给出的命令可能来自三个世界（CMD 的 `dir` / PowerShell 的 `Get-Process` / WSL 的 `apt`），统一终端把「判断该开哪个窗口」简化为「切一个标签」（原文 L114-124）。

## 边界与争议

- **统一窗口 ≠ 统一环境**：标签页只是并置，环境之间并不互通（路径、变量、权限各自独立）。原文的「走廊」比喻容易被误读为整合（原文 L44-46）。
- **观感论的可证伪性**：「好看降低门槛」是原文的经验主张（L142-146），本库暂无对照证据，**待验证**。
- 现代替代方向（本页尚未覆盖，待后续来源）：GUI 化的包管理、容器/开发容器、Windows 的 Dev Home 等。**待建**。

## 相关页面

- [[windows-terminal]]、[[command-prompt]]、[[powershell]]、[[wsl]]、[[ai-era-command-line]]、[[claude-code]]
- 来源：[[windows-terminal-tutorial]]

## 来源

- raw/Windows Terminal：把黑框变好看.md
