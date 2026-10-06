---
title: "Windows Terminal：把黑框变好看"
source: "https://mp.weixin.qq.com/s/kR6FJZ-jdRkxIhn9SBbvRw"
author:
  - "[[凡哥哥]]"
published:
created: 2026-10-06
description: "一个让人烦躁的日常你现在已经知道了三件事：CMD 是 Windows 的老命令行，跑 .bat 脚本和基础操作"
tags:
  - "clippings"
---
凡哥哥 光影紐扣 *Oct 4, 2026, 10:00 AM*

## 一个让人烦躁的日常

你现在已经知道了三件事：

- CMD 是 Windows 的老命令行，跑 `.bat` 脚本和基础操作。
- PowerShell 是现代命令行，处理复杂任务。
- WSL 是 Windows 里的真 Linux，跑 AI 工具。

于是你电脑上出现了三个黑框：CMD、PowerShell、Ubuntu（WSL）。

你要跑 CMD 命令，开一个 CMD。要跑 PowerShell，开一个 PowerShell。要跑 Linux 命令，开一个 Ubuntu。三个窗口堆在任务栏，切来切去，眼都花了。

更难受的是，这三个黑框长得还特别“复古”：白字黑底，字体模糊，不能分屏，不能调透明度，复制粘贴还别扭。

你心里想：都 2026 年了，怎么命令行还长这样？

微软也这么想。所以它做了一个东西：Windows Terminal。

今天我们就讲清楚：Windows Terminal 是什么，它怎么把黑框变好看，以及它为什么是 AI 时代命令行的“统一入口”。

## 一句话解释

Windows Terminal 是一个现代化的终端工具，能把 CMD、PowerShell、WSL 装进同一个窗口。

它不是替代它们。CMD 还是 CMD，PowerShell 还是 PowerShell，WSL 还是 WSL。Windows Terminal 只是给它们换了一个好看的“外壳”，让你在一个窗口里就能切换。

打个比方：

- CMD、PowerShell、WSL 是三间房子。
- 以前你每次只能进一间，出来再进另一间。
- Windows Terminal 是一条走廊，三间房子都开在走廊上，你走几步就能换一间。

这就是它的核心价值。

## 它长什么样

打开 Windows Terminal，你会看到：

- 一个窗口，上面有标签页。
- 默认标签可能是 PowerShell。
- 点旁边的下拉箭头，可以选择打开 CMD、PowerShell、WSL、Azure Cloud Shell 等。
- 每个标签页是一个独立会话，互不干扰。
- 窗口可以分屏，一边跑 PowerShell，一边跑 WSL。
- 可以调字体、配色、透明度、背景图。

简单说：它把命令行的颜值和易用性，拉到了现代水平。

## 一条最小命令：安装和打开

第一步：安装

Windows 11 已经自带 Windows Terminal。如果你用的是 Windows 10，可以：

- 打开 Microsoft Store，搜索“Windows Terminal”，点安装。
- 或者在 PowerShell 里输入：

```nginx
winget install Microsoft.WindowsTerminal
```

第二步：打开

按 Win 键，输入“Terminal”，回车。

或者右键桌面，选“在终端中打开”。

第三步：切换环境

点标签页旁边的下拉箭头，选：

- Windows PowerShell
- 命令提示符（CMD）
- Ubuntu（WSL）

你就看到不同环境的命令行了。

第四步：试试分屏

按 Alt + Shift + D，窗口分成左右两半。

左边跑 PowerShell，右边跑 WSL。你可以一边查 Windows 进程，一边跑 Linux 命令。

## 常用快捷键

| 快捷键 | 作用 |
| --- | --- |
| `Ctrl + Shift + T` | 新建标签页 |
| `Ctrl + Tab` | 切换标签页 |
| `Alt + Shift + D` | 分屏（左右） |
| `Alt + Shift + +` | 分屏（上下） |
| `Ctrl + Shift + W` | 关闭当前标签页 |
| `Ctrl + ,` | 打开设置 |
| `Ctrl + Shift + P` | 命令面板 |

不用全记。记住 Ctrl + Shift + T 和 Alt + Shift + D 就够日常用了。

## 为什么 AI 时代它特别有用

现在回到 AI 场景。

1\. 一个窗口，跑所有 AI 命令

AI 给你的命令，可能来自三个世界：

- CMD： `dir` 、 `ipconfig` 、`.bat` 脚本
- PowerShell： `Get-Process` 、系统管理
- WSL： `curl` 、 `apt` 、 `python` 、 `ollama`

以前你得判断“这是哪个环境的命令”，然后开对应窗口。

现在你只需要开 Windows Terminal，标签页切一下就行。甚至分屏，一边看教程，一边跑命令。

2\. 复制粘贴更顺手

AI 给你一段命令，你选中、复制、粘贴到 Windows Terminal 里。它支持标准快捷键：Ctrl + C 复制，Ctrl + V 粘贴。

老 CMD 窗口的复制粘贴逻辑很别扭，Windows Terminal 改掉了这个痛点。

3\. 分屏对照，减少出错

AI 给的步骤可能很长。你可以：

- 左边开一个 WSL，跑命令。
- 右边开一个 PowerShell，查状态。
- 上面开一个 CMD，看日志。

不用来回切窗口，减少“跑错环境”的概率。

4\. 好看，心情好

这不是玩笑。命令行本来就容易让人紧张。一个清晰、好看的终端，能降低心理门槛。

你不再觉得“这是黑客才用的东西”，而是“这是我电脑上的一个正常工具”。

## Windows Terminal 常用操作卡片

| 操作 | 快捷键 / 方法 | 作用 | 危险等级 |
| --- | --- | --- | --- |
| 新建标签页 | `Ctrl + Shift + T` | 开新会话 | 🟢 绿色 |
| 切换标签页 | `Ctrl + Tab` | 换环境 | 🟢 绿色 |
| 左右分屏 | `Alt + Shift + D` | 同屏对照 | 🟢 绿色 |
| 上下分屏 | `Alt + Shift + +` | 同屏对照 | 🟢 绿色 |
| 关闭标签页 | `Ctrl + Shift + W` | 关会话 | 🟢 绿色 |
| 打开设置 | `Ctrl + ,` | 调字体配色 | 🟢 绿色 |
| 命令面板 | `Ctrl + Shift + P` | 快速找功能 | 🟢 绿色 |
| 复制 | `Ctrl + C` | 复制选中内容 | 🟢 绿色 |
| 粘贴 | `Ctrl + V` | 粘贴内容 | 🟡 黄色 |

一句话总结：Windows Terminal 不是新命令，是新窗口。它把 CMD、PowerShell、WSL 装进一个好看的壳里，让你切换更方便、分屏更直观、复制粘贴更顺手。

## 避坑：三个注意

1\. 它不改变命令本身

Windows Terminal 只是外壳。CMD 命令还是 CMD 命令，Linux 命令还是 Linux 命令。别以为换了个好看的终端，命令就能通用了。

2\. 别在错误的标签页跑命令

你开了一个 PowerShell 标签，却粘贴了 Linux 命令，照样报错。先看标签页名字，再粘贴。

3\. 设置可以慢慢调

Windows Terminal 支持 JSON 配置文件，能改的东西很多。但别一上来就折腾配置。默认设置已经够用，先用起来，再慢慢调字体和配色。

## 一个建议：把默认终端改成 Windows Terminal

Windows 10/11 默认可能还是用老 CMD 窗口打开命令行。你可以改成 Windows Terminal：

- 打开 Windows Terminal。
- 按 `Ctrl + ,` 打开设置。
- 找到“启动” → “默认终端应用程序”。
- 选“Windows Terminal”。

以后你右键“在终端中打开”，或者从开始菜单打开命令行，都会用 Windows Terminal。

## 下一篇讲什么

今天你知道了 Windows Terminal 是命令行的统一入口，把 CMD、PowerShell、WSL 装进一个窗口，好看又好用。

明天我们进入第三周：Python 篇。

第一站：

为什么 AI 都爱写 Python？

为什么 AI 给你的脚本，十有八九是 Python？Python 到底有什么魔力，让 AI 这么偏爱它？搞懂这个，你就知道为什么本地要有 Python 环境。

---

下期预告：《为什么 AI 都爱写 Python？》

关键词：Python、解释器、AI 脚本、生态

命令卡片：

| 操作 | 快捷键 / 方法 | 作用 | 危险等级 |
| --- | --- | --- | --- |
| 安装 | `winget install Microsoft.WindowsTerminal` | 装 Windows Terminal | 🟡 黄色 |
| 新建标签 | `Ctrl + Shift + T` | 开新会话 | 🟢 绿色 |
| 切换标签 | `Ctrl + Tab` | 换环境 | 🟢 绿色 |
| 左右分屏 | `Alt + Shift + D` | 同屏对照 | 🟢 绿色 |
| 打开设置 | `Ctrl + ,` | 调外观 | 🟢 绿色 |
| 复制 / 粘贴 | `Ctrl + C`  / `Ctrl + V` | 复制粘贴 | 🟢 / 🟡 |

一句话总结：Windows Terminal 是命令行的“统一门面”。一个窗口，装下 CMD、PowerShell、WSL。AI 给命令，你切标签就能跑，不用再开三个黑框。