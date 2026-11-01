# github.com/clipperhouse/uax29/v2 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，并非官方原文副本。收件箱原文未修改；示例未在本机运行。

## 模块与来源

- 收件箱：`github.com/clipperhouse/uax29/v2`；官方模块：`github.com/clipperhouse/uax29/v2`。
- 用途：按 Unicode UAX #29 分割字素、单词和句子。
- [项目官方仓库](https://github.com/clipperhouse/uax29)；[所查官方文档](https://github.com/clipperhouse/uax29)；[Go Packages](https://pkg.go.dev/github.com/clipperhouse/uax29/v2)。
- [账号或组织主页](https://github.com/clipperhouse)用于身份核对，仓库所属不等于个人独立创作。

## 安装与典型用法

```sh
go get github.com/clipperhouse/uax29/v2/words
```

```go
words := words.FromString("Hello, 世界!"); for words.Next() { fmt.Println(words.Value()) }
```

## 边界

- 使用 v2 子包 import；分词边界按 Unicode 标准，不等于应用语义词。
- 版本由目标项目锁定；示例未在本机下载或编译。
