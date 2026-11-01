---
title: "go.yaml.in/yaml/v2 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/yaml-v2-go-official-research-2026-11-01.md]
author: "官方项目与 Go Packages；Codex 整理"
source_url: "https://pkg.go.dev/go.yaml.in/yaml/v2"
raw_file: "raw/yaml-v2-go-official-research-2026-11-01.md"
format: notes
---

# go.yaml.in/yaml/v2 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [Go Packages](https://pkg.go.dev/go.yaml.in/yaml/v2) 和 [官方仓库](https://github.com/go-yaml/yaml)；研究笔记 `raw/yaml-v2-go-official-research-2026-11-01.md` 不是官方原文副本。

## 一句话概括

> 将 YAML 编解码为 Go 值，提供严格解码以发现未知字段和重复键。

## 核心要点

- 典型 API：`var cfg struct { Name string `yaml:"name"` }`。（raw「典型 API」）
- 关键边界：官方项目明确标为 unmaintained，仓库已归档；当前路径是 go.yaml.in/yaml/v2，旧 gopkg.in 路径须另行核对。（raw「关键边界与待验证」）
- 身份证据：官方 README 由 Gustavo Niemeyer 自述为早期项目并声明停止维护。（raw「创建者、维护者和关联」）

## 与既有知识的关系

- 该模块扩展本库 Go 第三方库索引。
- 创建者或维护范围不能由仓库归属单独推断；未知处已标待验证。

## 由本来源派生 / 更新的页面

- [[yaml-v2-go]]、[[gustavo-niemeyer]]。
